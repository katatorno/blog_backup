---
title: "Pressure and temperature reading from BMP280 sensor on Raspberry Pi"
datePublished: Sun May 18 2025 12:04:55 GMT+0000 (Coordinated Universal Time)
cuid: cmatlztbh000409jybhs8fkb5
slug: pressure-and-temperature-reading-from-bmp280-sensor-on-raspberry-pi
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1747569782286/937b2e1f-690b-4c4a-8b3e-69b0e7732ada.jpeg
tags: raspberry-pi, pressure-sensor, temperature-sensor, bmp280

---

Raspberry OS is installed, everything booted up — now it’s time to breathe some life and meaning into this piece of silicon with an operating system. The reasons for starting this project, apart from learning the Raspberry platform with a long-term plan of mastering Yocto, included monitoring weather conditions — especially atmospheric pressure. I’d like to keep a record of pressure in the places where I live to try and confirm or disprove my observations — my mood seems to fluctuate along with the pressure. Atmospheric pressure data should be available online, but I wasn’t able to find a site with very local data and easy access to historical records. In my opinion, learning for the sake of learning is pointless — personally, I find it hard to stay motivated if there’s no specific goal behind it. If there’s a strong desire to learn but no goal — find one. Let’s treat this goal as my motivator for learning — without diving into the details of whether the whole project even makes sense.

What are my assumptions about the sensor itself? Very simple - it has to be cheap, measure pressure, it would be nice if it also measured temperature, and it has to be widely used - I don't want to write controllers from scratch. I settled on the BMP280 sensor. It meets all the requirements!

The sensor can measure pressure from 300 to 11000 hPa and temperature from -40 to 85 °C. I can communicate with it via I2C and SPI interfaces. Libraries, examples and development boards are available.

![BME280 sensor](https://cdn.hashnode.com/res/hashnode/image/upload/v1747568916835/a68b7828-005f-4aae-a7d9-2a402fa33c6c.jpeg align="center")

I will connect the sensor to the Raspberry via the I2C bus, which is a serial and synchronous bus using two communication lines:

* **SCL** \- the clock line, which, like a conductor, sets the rythm of communication,
    
* **SDA** \- the line on which the actual communication takes place.
    

Besides the communication lines, the **GND** (ground) line must be connected — you need to know the reference point against which to measure the potentials on the lines.

The sensor needs to know which bus to use - there is a choice of I2C and SPI buses. The **CSB** line is used to select the bus: a logic 1 (3.3 V) state selects the I2C bus, while a logic 0 (0 V) state selects the SPI bus. Below I show the sensor connection from my Raspberry Pi to the I2C1 interface.

![Raspberry Pi Pinout Guide: How to use the Raspberry Pi GPIOs ...](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2023/03/Raspberry-Pi-Pinout-Random-Nerd-Tutorials.png?quality=100&strip=all&ssl=1 align="left")

| **BMP280** | **Raspberry** |
| --- | --- |
| VCC | 01 |
| GND | 39 |
| SCL | 05 |
| CDA | 03 |
| CSB | 17 |
| SDO | NC |

After connecting everything, we need to enable the I2C bus. We can do this in two ways — through the graphical interface:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747489267595/159511cd-d0f6-4f3f-af56-59a91d3b7209.png align="left")

Or via the command line:

```bash
sudo raspi-config
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747569503094/9372eb5d-0ffb-43d6-9563-f07735ea0052.jpeg align="center")

I had some minor issues getting the sensor started, so I’d suggest rebooting the Raspberry after enabling the interface.

The next step should be to verify if we connected the sensor correctly and if we can find its address. For that, we’ll need the tool **i2cdetect**.

```bash
sudo apt update
sudo apt install -y i2c-tools
```

We connected the device to the I2C1 bus — dedicated for connecting external sensors. I2C0 is reserved for the Raspberry hat with EEPROM. To find the sensor on the I2C1 bus, use the following command:

```bash
i2cdetect -y 1
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747569594740/64c94b87-3c82-428f-92e0-c63dd3ca55b5.jpeg align="center")

Success! The sensor is available at address **0x76**!

So let’s write some simple code to read the sensor’s parameters: pressure and temperature! Let’s create a project folder, start a virtual environment, install a [ready-made Python library](https://pypi.org/project/bmp280/), and create a script file:

```bash
mkdir temppressread
cd temppressread/
python -m venv temppressread
source temppressread/bin/activate
pip install bmp280
touch run.py
```

Using [the examples available on the library’s website](https://github.com/pimoroni/bmp280-python/tree/main/examples), let’s create a simple script to read temperature and pressure, then run it!

```python
#!/usr/bin/env python

import time
from smbus2 import SMBus
from bmp280 import BMP280
from datetime import datetime

# Initialise the BMP280
bus = SMBus(1)
bmp280 = BMP280(i2c_dev=bus)

while True:
    now = datetime.now()
    formatted = now.strftime("%y-%m-%d %H:%M:%S")
    temperature = bmp280.get_temperature()
    pressure = bmp280.get_pressure()
    print(formatted,f" -  {temperature:05.2f}*C {pressure:05.2f}hPa")
    time.sleep(1)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747569745720/601d4c22-9da3-4bf4-a7a5-32783471eebc.jpeg align="center")

The sensor and the script are working! Next, I’ll try installing Home Assistant on the Raspberry and somehow connect this data so I can track it with nice charts and monitor the historical data!