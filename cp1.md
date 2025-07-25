# Checkpoint 1
[Interactive - Checkpoint 1](https://makecode.microbit.org/#tutorial:github:planeson/husky-car-tutorial/cp1)  
## HuskyLens
Follow the instructions and learn how to use HuskyLens first, then come back to this section.  

## Implementation
### Set up!
Now that you have connected the HuskyLens to your BBC micro:bit, start by initializing your HuskyLens using your micro:bit. From the ``||huskylens:HuskyLens||`` category, insert a ``||huskylens:HuskyLens initialize I2C until success||`` block into the ``||basic:on start||`` block. You should also insert a ``||huskylens:HuskyLens switch algorithm to Object Tracking||`` block to set HuskyLens into object tracking mode. Insert the ``||pksdriver:motor M1 dir CW speed 0||`` block inside the *Edu Kit* category to ensure both motors, *M1* and *M2* turns off. You can also add two different icon with ``||basic:show icon||`` at the beginning and end of the ``||basic:on start||`` block to give an indication on the state of the car.   
```blocks
basic.showIcon(IconNames.Heart)
pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CCW, 0)
huskylens.initI2c()
huskylens.initMode(protocolAlgorithm.ALGORITHM_OBJECT_TRACKING)
basic.showIcon(IconNames.Yes)
```

## Get Moving!
You need to keep looking for the object. If the object is found, turn both motors clockwise (CW) to a speed of 40, and turn off the LED at pin P0. If the object isn't found, turn both motors to a speed of 0, then turn on the LED at pin P0. To tell the HuskyLens to go look for the object you taught it, use the ``||huskylens:HuskyLens request data once and save into the result||`` block. The ``||huskylens:HuskyLens check if frame is on screen from the result||`` block will tell you whether HuskyLens have found the object it learnt. With the ``||logic:if else||`` block, you can tell the micro:bit to do different things when the object is found and when the object isn't found. In case you forgot, you can use the ``||pksdriver:motor M1 dir CW speed 0||`` block inside the *Edu Kit* subcategory to set a motor's speed, and you can use the ``||pins:digital write pin P0 to 1||`` block to turn on/off an LED connected to pin P0.
```blocks
basic.forever(function () {
    huskylens.request()
    if (huskylens.isAppear_s(HUSKYLENSResultType_t.HUSKYLENSResultBlock)) {
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 40)
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, 40)
        pins.digitalWritePin(DigitalPin.P0, 0)
    } else {
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, 0)
        pins.digitalWritePin(DigitalPin.P0, 1)
    }
})
```
## Conclusion
Congrats! Your car now goes forward when a recognized object is found. If it isn't found, it stops and lights an LED.  

[\[Interactive\] - Checkpoint 2](https://makecode.microbit.org/#tutorial:github:planeson/husky-car-tutorial/cp2)  
[\[GitHub Pages\] - Checkpoint 2](https://planeson.github.io/husky-car-tutorial/cp2)  
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
