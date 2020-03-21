The Sonoff iFan02 is supported in Tasmota from version 6.0.0b

* [Itead Product Page](http://sonoff.itead.cc/en/products/appliances/sonoff-ifan02)
* [Itead Shop](https://www.itead.cc/sonoff-ifan02-wifi-smart-ceiling-fan-with-light.html)
* [Itead iFan02 Schematics](https://github.com/arendst/arendst.github.io/blob/master/media/ifan02/iFan02Schematics.pdf)

## Serial Flashing

Please see the [Hardware Preparation](installation/Hardware-Preparation) page for general instructions.

Flashing using only a USB to serial converter will not work as the unit draws too much current as can be observed by a flashing blue led on the PCA and a lot of serial gibberish. As AC is not connected to Gnd I used the available power supply of the unit and connecting the USB to serial converter to J3 pins Gnd, Tx and Rx.

The button is not connected to GPIO0 so flashing the unit requires some extra work. I managed to flash the iFan02 by soldering a wire to TP16 (GPIO00) on the bottom of the PCA. Keep this wire connected to Gnd during the power-on or reset process (pressing the button) and the unit will be in firmware upgrade mode. If you've soldered the gpio0 connection don't forget to unsolder before booting normally.  

Connect RX -> TX | 3.3 -> 3.3 | TX -> RX | GND -> GND  and connect TP16 to GND (as used in the TTL). 

Press and hold the button while connecting to power.

![](https://user-images.githubusercontent.com/34340210/57892049-9f0e5200-780b-11e9-9beb-14125dd9d4c9.jpg)

> If you have an Arduino you may be able to flash without providing an additional power source. I have successfully flashed using an Arduino Duemilanove with the atmel chip pulled out (basically using it for FTDI and 3.3v power regulation). Rx on Arduino goes to Rx on iFan02, Tx to Tx (no crossover like with FTDI). I did not have to press the button, only to ground TP16 while initiating the flash in Arduino IDE. The Arduino provides enough power to flash, however it will not boot into Tasmota unless you plug in to external power (it boot loops after flashing is complete).

## Additonal information
* See issue [#2839](https://github.com/arendst/Tasmota/issues/2839) for user information
* See issue [#3412](https://github.com/arendst/Tasmota/issues/3412) light on after restore power

Functioning iFan02 in Tasmota WebUI

<img src="https://user-images.githubusercontent.com/32016319/42774826-69493298-8950-11e8-8d7c-080df49d584f.png" alt="drawing" width="300">

iFan02 PCA with TP16 

<img src="https://user-images.githubusercontent.com/32016319/42733081-30196220-8849-11e8-8c97-e3aa31796d47.png" alt="drawing" width="300px">

Two users report the TP16 pad lifting after soldering a wire to ground as shown in picture.  This renders it useless.  It may be better to use a pogo pin contact, bare wire or solder and then epoxy/glue the wire in place, leaving it permanently.

Board Top Showing ESP8285

![UNSHIELDED Board Top Showing ESP8285](https://user-images.githubusercontent.com/24206271/42735638-e8f4ac6a-8825-11e8-8fa8-84d4edc633a6.png)

ESP8285 Pinout 

![esp8285 PINOUT](https://user-images.githubusercontent.com/24206271/42735641-ec448494-8825-11e8-82e8-78d97bd3a087.png)

### Using hard wired push button switch attached to iFan02 GPIO to cycle speeds

If anyone wants to setup a single push button switch attached to the GPIO3 Serial + ground In that will cycle through the speeds and turn off - after setting it in the configuration (GPIO3 to 11 Switch3) the console code is: 

`rule1 on switch3#state do FanSpeed + endon`

### Alternate Power Supply Schematic

![esp8285 PINOUT](https://user-images.githubusercontent.com/24206271/43140236-857bc724-8f21-11e8-87c0-6f3688cb5eb0.gif)

