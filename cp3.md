# Checkpoint 3

## Slow is smooth, smooth is fast.
To ensure accuracy, slow the car down when the object is close, but speed it back up if it is far away!  
Use the *HuskyLens get width of ID 1 frame from the result* block to determine roughly how far the object is away from the car.  
You can use the ``||huskylens:HuskyLens get width of ID 1 frame from the result||`` block to get the width value. You may also want the ``||variables:Variables||`` ``|Make a Variable|`` block to create a variable named `Speed`, the ``||math:arithmetic||`` block for calculations, the ``||pksdriver:motor M1 dir CW speed 0||``block to control the motors, and the ``||pins:digital write pin P0 to 0||`` block to control the LED.
```blocks
let speed = 0
basic.forever(function () {
    huskylens.request()
    if (huskylens.isAppear_s(HUSKYLENSResultType_t.HUSKYLENSResultBlock)) {
        speed = 255 - huskylens.readeBox(1, Content1.width)
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0.3 * speed)
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, 0.3 * speed)
        pins.digitalWritePin(DigitalPin.P0, 0)
    } else {
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, 0)
        pins.digitalWritePin(DigitalPin.P0, 1)
    }
})
```

## Assessment
### It all comes together!
Implement the entire object-tracking car.  
Like in [checkpoint 2](/husky-car-tutorial/cp2), use a variable, which you can name *delta*, to store the difference between the centre of the frame and the centre of the display (160).  
You can use the ``||huskylens:HuskyLens get X center of ID 1 frame from the result||`` block to get the X center value, the ``||variables:Variables||`` ``|variables:Make a Variable|`` block to create a variable named delta, the ``||math:arithmetic||`` block for calculations, the ``||pksdriver:motor M1 dir CW speed 0||`` block to control the motors, and the ``||pins:digital write pin P0 to 0||`` block to control the LED.
Set the left motor CW at speed of 0.3 * *(speed+delta)*, the right motor also CW but at 0.3 * *(speed-delta)*. Turn the LED off.  
If the object isn't found, set both motors to speed 0, and turn the LED back on.  
```blocks
let speed = 0
let delta = 0
basic.forever(function () {
    huskylens.request()
    if (huskylens.isAppear_s(HUSKYLENSResultType_t.HUSKYLENSResultBlock)) {
        speed = 255 - huskylens.readeBox(1, Content1.width)
        delta = huskylens.readeBox(1, Content1.xCenter) - 160
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0.3 * (speed + delta))
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, 0.3 * (speed - delta))
        pins.digitalWritePin(DigitalPin.P0, 0)
    } else {
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, 0)
        pins.digitalWritePin(DigitalPin.P0, 1)
    }
})
```
## Conclusion
Congrats! Your car now tracks an object around! You can fine the the numbers around to make its performance better, like giving a multiplier to `delta` / `speed`.  
Extended thinking - how difficult would tracking an object be if you don't have AI to learn the appearance of objects? Is it even possible?  
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
