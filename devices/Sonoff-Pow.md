Sonoff Pow has been obsoleted with [Sonoff Pow R2](https://blakadder.github.io/sonoff_dual_R2.html). Before configuring your device check which revision you have.

## ⚠️️Special Attention   ⚠️️

**Do not connect AC power and the serial connection at the same time** 
The GND connection of the Pow is connected to the live AC wire. Connecting serial with your PC will fry your PC and will electrocute you. 

**DO NOT CONNECT ANYTHING TO THESE DEVICES!!! (No sensors, no switches, nothing) <br>
The GPIOs on the Pow are connected to AC power!** Only use a POW as designed. 

**The AC connection between Pow and Pow R2 is different**, please check exactly which version you have.
- **Pow R2**: Lo-E-E-Li-N-N = LineOut-EarthOut-EarthIn-LineIn-NeutralOut-NeutralIn
- **Pow**: Lo-E-E-N-N-Li = LineOut-EarthOut-EarthIn-NeutralOut-NeutralIn-LineIn

## Serial Connection 

Please see the [Hardware Preparation](installation/Hardware-Preparation) page for general instructions.

3V3, RX, TX and GND pins are available at the rear end of the PCB.

![](https://user-images.githubusercontent.com/5904370/57881749-5f069980-7822-11e9-9438-95650ea42a20.png)

To enter **flash mode**, press down on the button while powering the device.

## Power Monitoring Calibration
Sonoff Pow might need calibration as correct measurements are influenced by hardware and timing differences. See [Power Monitoring Calibration](/Power-Monitoring-Calibration)
   
## Telemetry
The Sonoff Pow can provide Energy, Power, Voltage and Current information in different ways.

The preferred way is using the periodic telemetry data. Default setting ```TelePeriod 300``` will send telemetry data every 5 minutes.<br />
> If the setting `PowerDelta` (new since version 5.12.0e) is not 0 (default 80%), telemetry will be sent on power change too.

```
tele/pow1/SENSOR = {"Time":"2018-02-15T17:37:10","ENERGY":{"TotalStartTime":"2018-11-14T18:39:40","Total":6.294,"Yesterday":5.340,"Today":0.954,"Period":217,"Power":2635,"ApparentPower":2650,"ReactivePower":282,"Factor":0.99,"Voltage":227,"Current":11.661}}
```

To request information you can use command `Status 8`.
```
stat/pow1/STATUS8 = {"StatusSNS":{"Time":"2018-11-15T08:54:18","ENERGY":{"TotalStartTime":"2018-11-14T18:39:40","Total":6.404,"Yesterday":5.340,"Today":1.064,"Power":2629,"ApparentPower":2645,"ReactivePower":288,"Factor":0.99,"Voltage":226,"Current":11.677}}}
```

The presented information has the following meaning:
```
Message        | Unit | Description
---------------|------|-----------------------------------------------------
TotalStartTime | Date | DateTime of calculation for Total
Total          | kWh  | Total Energy usage including Today
Yesterday      | kWh  | Total Energy usage between 00:00 and 24:00 yesterday
Today          | kWh  | Total Energy usage today from 00:00 until now
Period         | Wh   | Energy usage between previous message and now
Power          | W    | Current effective power load
ApparentPower  | W    | Power load on the cable = sqrt(Power^2 + 
               |      | ReactivePower^2)
ReactivePower  | W    | Reactive load
Factor         |      | The ratio of the real power flowing to the load to
               |      | the apparent power in the circuit 
Voltage        | V    | Current line voltage
Current        | A    | Current line current
```

## Self Protection for Sonoff Pow

ITEAD published a recall notice for the Sonoff Pow on March 1st 2017. Some units produced in december 2016 and january 2017 are not well suited for 16A. If you have one of these units you can decide to use them anyway by limiting the maximum current in software.
It is, in fact,  possible to set a Maximum Power Threshold for the Sonoff Pow.

 If the power measured by the device exceeds the threshold set by the command `MaxPower` for a number of seconds set by the command `MaxPowerHold` the device will remain switched off for `MaxPowerWindow` seconds (to let it cool down, for example).

For all details see [issue #218](https://github.com/arendst/Tasmota/issues/218)

## Official Sources

* [Itead Product Page](http://sonoff.itead.cc/en/products/sonoff/sonoff-pow)
* [Itead Shop](https://www.itead.cc/sonoff-pow.html)
* [Itead Wiki](https://www.itead.cc/wiki/Sonoff_Pow)
