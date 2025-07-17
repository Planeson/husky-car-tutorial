# Checkpoint 2
[Interactive - Checkpoint 2](https://makecode.microbit.org/#tutorial:github:planeson/husky-car-tutorial/cp2)
## Right to be left? Left to be right?
We want to turn the car towards the object.  
Use the ``||huskylens:HuskyLens get X center of ID 1 frame from the result||`` block to determine whether to turn left or right. Hint: the centre of the screen is at x=160. You can check if the X centre is larger or smaller than 160.  
```blocks
basic.forever(function () {
    huskylens.request()
    if (huskylens.isAppear_s(HUSKYLENSResultType_t.HUSKYLENSResultBlock)) {
        if (huskylens.readeBox(1, Content1.xCenter) > 160) {
            basic.showLeds(`
                . . # . .
                . . . # .
                # # # # #
                . . . # .
                . . # . .
                `)
        } else {
            basic.showLeds(`
                . . # . .
                . # . . .
                # # # # #
                . # . . .
                . . # . .
                `)
        }
    }
    else
    {
        basic.showIcon(IconNames.No)
    }
})
```

## Turn to the left in threes, left turn!
Turn towards the object.  
Use a variable, which you can name *delta*, to store the difference between the centre of the frame and the centre of the display (160).  
Set the left motor CW at speed of 0.4 * *delta*, the right motor also CW but at -0.4 * *delta*. Turn the LED off.  
If the object isn't found, set both motors to speed 0, and turn the LED back on.  
You can use the ``||variables:Variables||`` ``|Make a Variable|`` button to make a new variable with any name of your choosing, ``||variables:set delta to||`` block to set a variable, the ``||math:arithmetic||`` block for calculations, the ``||pksdriver:motor M1 dir CW speed 0||`` block to control the motors, and the ``||pins:digital write pin P0 to 0||`` block to control the LED.
```blocks
let delta = 0
basic.forever(function () {
    huskylens.request()
    if (huskylens.isAppear_s(HUSKYLENSResultType_t.HUSKYLENSResultBlock)) {
        delta = huskylens.readeBox(1, Content1.xCenter) - 160
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0.4 * delta)
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, -0.4 * delta)
        pins.digitalWritePin(DigitalPin.P0, 0)
    } else {
        pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
        pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CW, 0)
        pins.digitalWritePin(DigitalPin.P0, 1)
    }
})
```
## Conclusion
Congrats! Your car now goes turns towards the recognized object.  

[\[Interactive\] - Checkpoint 3](https://makecode.microbit.org/#tutorial:github:planeson/husky-car-tutorial/cp3)  
[\[GitHub Pages\] - Checkpoint 3](https://planeson.github.io/husky-car-tutorial/cp3)  
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
