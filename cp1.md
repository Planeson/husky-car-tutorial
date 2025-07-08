# Checkpoint 1
## HuskyLens
Follow the instructions and learn how to use HuskyLens first, then come back to this section.  

## Implementation
### Set up!
Now that you have connected the HuskyLens to your BBC micro:bit, start by initializing your HuskyLens using your micro:bit.  
```blocks
basic.showIcon(IconNames.Heart)
pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CCW, 0)
huskylens.initI2c()
huskylens.initMode(protocolAlgorithm.ALGORITHM_OBJECT_TRACKING)
basic.showIcon(IconNames.Yes)
```

## Get Moving!
You need to keep looking for the object.  
If the object is found, turn both motors clockwise (CW) to a speed of 40, and turn off the LED at pin P0.  
If the object isn't found, turn both motors to a speed of 0, then turn on the LED at pin P0.  
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
Congrats! Your car now goes forward when a recognized object is found. If it isn't found, it stops and lights and LED.  

[Checkpoint 2](/husky-car-tutorial/cp2)  
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
