# mh-z19
Read CO2 concentration from mh-z19 sensor

![MH-Z19](https://camo.githubusercontent.com/8456a67ab97a13866d928d3a14dff59a57cdeccb/68747470733a2f2f63616d6f2e716969746175736572636f6e74656e742e636f6d2f613237306466313136326564356333626639393638623234303634623931656564306466636331312f3638373437343730373333613266326637313639363937343631326436393664363136373635326437333734366637323635326537333333326536313664363137613666366536313737373332653633366636643266333032663334333633353334333432663331333533373339363633393634363232643330363633343330326433373336363533383264333033353636333332643339333933333631333233343633333433373634333133383265373036653637)

## install
```
pip install mh-z19
```
## installs
[![Downloads](https://pepy.tech/badge/mh-z19)](https://pepy.tech/project/mh-z19)
[![Downloads](https://pepy.tech/badge/mh-z19/month)](https://pepy.tech/project/mh-z19)
[![Downloads](https://pepy.tech/badge/mh-z19/week)](https://pepy.tech/project/mh-z19)

## how to use
Use as python script.
```
pi@raspberrypi:~/mh-z19/pypi $ sudo python -m mh_z19
{'co2': 500}
```

Import module and call read()
```
pi@raspberrypi:~/mh-z19/pypi $ sudo python
Python 2.7.13 (default, Nov 24 2017, 17:33:09) 
[GCC 6.3.0 20170516] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import mh_z19
>>> mh_z19.read()
{'co2': 477}
>>> 
```

The ***sudo*** might be necessary because mh_z19 module use Serial.

The differences of the interface between each Raspberry Pi modle are resolved inside this module. For example, serial device name is difference between Raspberry Pi 3 and older model, but mh-z19 module automatically detect the model and read from appropriate serial device.

To use mh-z19, once you need to set up enabling serial port device on the Raspbyerr Pi.
Following [Wiki](https://github.com/UedaTakeyuki/mh-z19/wiki/How-to-Enable-Serial-Port-hardware-on-the-Raspberry-Pi) page might be informative.

## cabling
Connect RPi & mh-z19 as:

- 5V on RPi and Vin on mh-z19
- GND(0v) on RPi and GND on mh-z19
- TxD and RxD are connect to cross between RPi and mh-z18 

Followings are example of cabling, but you can free to use other 5v and 0v Pin on the RPi. 

![Cabling](https://camo.githubusercontent.com/3cd4c1b482ea902b7e66dca13d4260193c831a63/68747470733a2f2f63616d6f2e716969746175736572636f6e74656e742e636f6d2f313132616435666534316338326131363637316432383832303730333834313039633838363063632f36383734373437303733336132663266373136393639373436313264363936643631363736353264373337343666373236353265373333333265363136643631376136663665363137373733326536333666366432663330326633343336333533343334326633303338333233383333333033313334326433363338363433323264363333333634363532643331333633343334326433373633333836343339363233373632333633323636363432653661373036353637)

```
pi@raspberrypi:~/mh-z19 $ gpio readall
 +-----+-----+---------+------+---+---Pi B+--+---+------+---------+-----+-----+
 | BCM | wPi |   Name  | Mode | V | Physical | V | Mode | Name    | wPi | BCM |
 +-----+-----+---------+------+---+----++----+---+------+---------+-----+-----+
 |     |     |    3.3v |      |   |  1 || 2  |   |      | 5v      |     |     |
 |   2 |   8 |   SDA.1 |   IN | 1 |  3 || 4  |   |      | 5v      |     |     |  <---- Vin
 |   3 |   9 |   SCL.1 |   IN | 1 |  5 || 6  |   |      | 0v      |     |     |  <---- Gnd
 |   4 |   7 | GPIO. 7 |   IN | 1 |  7 || 8  | 1 | ALT0 | TxD     | 15  | 14  |  <---- RxD
 |     |     |      0v |      |   |  9 || 10 | 1 | ALT0 | RxD     | 16  | 15  |  <---- TxD
 |  17 |   0 | GPIO. 0 |   IN | 0 | 11 || 12 | 0 | IN   | GPIO. 1 | 1   | 18  |
 |  27 |   2 | GPIO. 2 |   IN | 0 | 13 || 14 |   |      | 0v      |     |     |
 |  22 |   3 | GPIO. 3 |   IN | 0 | 15 || 16 | 0 | IN   | GPIO. 4 | 4   | 23  |
 |     |     |    3.3v |      |   | 17 || 18 | 0 | IN   | GPIO. 5 | 5   | 24  |
 |  10 |  12 |    MOSI |   IN | 0 | 19 || 20 |   |      | 0v      |     |     |
 |   9 |  13 |    MISO |   IN | 0 | 21 || 22 | 0 | IN   | GPIO. 6 | 6   | 25  |
 |  11 |  14 |    SCLK |   IN | 0 | 23 || 24 | 1 | IN   | CE0     | 10  | 8   |
 |     |     |      0v |      |   | 25 || 26 | 1 | IN   | CE1     | 11  | 7   |
 |   0 |  30 |   SDA.0 |   IN | 1 | 27 || 28 | 1 | IN   | SCL.0   | 31  | 1   |
 |   5 |  21 | GPIO.21 |   IN | 1 | 29 || 30 |   |      | 0v      |     |     |
 |   6 |  22 | GPIO.22 |   IN | 1 | 31 || 32 | 0 | IN   | GPIO.26 | 26  | 12  |
 |  13 |  23 | GPIO.23 |   IN | 0 | 33 || 34 |   |      | 0v      |     |     |
 |  19 |  24 | GPIO.24 |   IN | 0 | 35 || 36 | 0 | IN   | GPIO.27 | 27  | 16  |
 |  26 |  25 | GPIO.25 |   IN | 0 | 37 || 38 | 0 | IN   | GPIO.28 | 28  | 20  |
 |     |     |      0v |      |   | 39 || 40 | 0 | IN   | GPIO.29 | 29  | 21  |
 +-----+-----+---------+------+---+----++----+---+------+---------+-----+-----+
 | BCM | wPi |   Name  | Mode | V | Physical | V | Mode | Name    | wPi | BCM |
 +-----+-----+---------+------+---+---Pi B+--+---+------+---------+-----+-----+
```

### Q&A
Any questions, suggestions, reports are welcome! Please make [issue](https://github.com/UedaTakeyuki/mh-z19/issues) without hesitation! 

## history
- 0.1.1  2018.11.05  first version self-forked from [slider](https://github.com/UedaTakeyuki/slider).
- 0.1.3  2018.11.06  fix Readme.
- 0.1.4  2018.11.15  revise Readme.
- 0.1.6  2018.11.29  revise Readme.
