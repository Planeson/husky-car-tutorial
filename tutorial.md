# Object-tracking car
## Step 1
### HuskyLens
Follow the instructions and learn how to use HuskyLens first, then come back to this section.

## Step 2
### Implementation
### set up
Now that you have connected the HuskyLens to your BBC micro:bit, start by initializing your HuskyLens using your micro:bit.
```block
let delta = 0
let speed = 0
basic.showIcon(IconNames.Heart)
pksdriver.MotorRun(pksdriver.Motors.M1, pksdriver.Dir.CW, 0)
pksdriver.MotorRun(pksdriver.Motors.M2, pksdriver.Dir.CCW, 0)
huskylens.initI2c()
huskylens.initMode(protocolAlgorithm.ALGORITHM_OBJECT_TRACKING)
basic.showIcon(IconNames.Yes)
```
## Step 3
### forever
You need to keep looking for the object. Use this block to retrieve data from the HuskyLens.
```block
huskylens.request()
```
