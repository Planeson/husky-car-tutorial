# Object-tracking car
## HuskyLens
Follow the instructions and learn how to use HuskyLens first, then come back to this section.

## Implementation
### set up
Now that you have connected the HuskyLens to your BBC micro:bit, start by initializing your HuskyLens using your micro:bit.
```blocks
basic.showIcon(IconNames.Heart)
pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CCW, 0)
huskylens.initI2c()
huskylens.initMode(protocolAlgorithm.ALGORITHM_OBJECT_TRACKING)
basic.showIcon(IconNames.Yes)
```

## forever
You need to keep looking for the object. Use this block to retrieve data from the HuskyLens.
```blocks
huskylens.request()
```
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
