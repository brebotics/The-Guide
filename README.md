# The Guide
Become Not Stupid™

wuz gud guyz, its ya boy

dis gyde is 4 ftc teams 

## Setting up Android Studio
head ova to da [android studio website](https://developer.android.com/studio), n download da exe

make sure ur not on a firewalled wifi connection, gradle issues may occur


now that android studio is installed, i assume you want to learn roadrunner as well. download [roadrunner from da github](https://github.com/acmerobotics/road-runner)

open the project with AS(android studio)
## Previous Projects
If continuing from last year, make sure to backup your code on a seperate folder, as well as on github. 

Yoink da teleop & auto files

also make sure to update versions so that control hub & robot controller are the same version

## TeleOp
copy da files either from previous year or [INPUT ORIGIN HERE](chrome://dino/)

make sure to UPDATE the variables to ur current build: if the robot has 4 wheels or 6 wheels, if the robot has a claw or a shooter, and make sure that **you have x & y variables to move**

ex: basic DriveTrain code
```
package org.firstinspires.ftc.teamcode;

import ...

@TeleOp(name = "very gracious professional")
public class ProvTele extends LinearOpMode {
double x;
double y;
double rx;
```
...
```
public void runOpMode() {
...
    Right_Front = hardwareMap.get(DcMotorEx.class, "rightFront");
    Right_Rear = hardwareMap.get(DcMotorEx.class, "rightRear");
    Left_Front = hardwareMap.get(DcMotorEx.class, "leftFront");
    Left_Rear = hardwareMap.get(DcMotorEx.class, "leftRear");

...
    if (opModeIsActive()) {
        while (opModeIsActive()) {
            y = gamepad1.left_stick_y;
            x = -gamepad1.left_stick_x * 1.1;
            rx = -gamepad1.right_stick_x;
            
            Left_Front.setPower((y + x + rx) * constant);
            Left_Rear.setPower((y - x + rx) * constant);
            Right_Front.setPower((y - x - rx) * constant);
            Right_Rear.setPower((y + x - rx) * constant);
...
    }
}
...
}
```
modify code is seen fit
ex: Last Years code (in da rep)

## Autonomous
***FIRST, VERY IMPORTANT: READ THE ***[***ROADRUNNER WEBSITE***](https://learnroadrunner.com/)
very important to READ over and not skim over important parts
one mistake we made was skimming over the DriveConstants part, where we did not confirm with the builders what gear ratio we used. 

copy the ConceptTensorFlowObjectDetectionWebcam.java from *FtcRobotController/java/.../external/samples* into *TeamCode/java/.../teamcode/*

(using the tfodWebcam file, cuz i assume you wanna learn object detection aswell) (the comments IN the file show you the basics of object detection)

under the **while (opModeIsActive())** bracket, ***AFTER*** the **if statement** put in your code.

learn obute trajectorie on da website 

## Tuning
***VERY IMPORTANT: READ THE ***[***ROADRUNNER WEBSITE***](https://learnroadrunner.com/)
```bash
1. Import the FTC project in Android Studio
2. Connect your device with the robot
3. press play button in Android Studio to build and upload the code.
```

[Installing Road Road Runner onto Android Studio](https://learnroadrunner.com/installing.html#method-1-downloading-the-quickstart)

This is the appropriate steps for the android studio

```bash
1. DriveConstants
2. DriveFeedforwardTuner (found as AutomaticFeedforwardTuner)
3. StraightTest & StrafeTest
4. TrackWidthTuner
5. TurnTest
6. FollowerPIDTuner
7. SplineTest
```

Before tuning, if 192.168.43.1:8080/dash link doesn't work it either means you haven't installed Road Runner properly or your robot is not connected
This is a helpful video for the first few tests: [video](https://www.youtube.com/watch?v=7wjaX2KXrrM)

### 1. DriveConstants

Make sure to get this step right.
If you get this step wrong you will end up having trouble with the rest of the tests
(This is what we were stuck on for a while)

### 2. DriveFeedForwardTuner

```bash
BEFORE YOU START 
The robot most likely WILL drift this is NOT AN ISSUE
just make sure that the graph is close to accurate and you are good to move on

kV: affect the max and min of the graph
kA: affects the phase shift of the graph. Changing the kA will make the graph horizantally aligned with the target graph.
!!!!!(Start with a very small number and increase bit by bit or else the robot may go insane)!!!!!
kStatic: We just used the value from the AutomaticFeedforwardTuner

The graph will have a small lump, just ignore it it's REV's fault.
```

First, start with the AutomaticFeedforwardTuner to find the approximate value of the kV and kStatic.
You will need to use your phone and controller for the telemetry.
(The MAX_VEL should be 1/(kV) if it is not the case, change the MAX_VEL value not the kV.)

Then, run the ManualFeedforwardTuner with the values you got. From there, tinker the values until the graph is somewhat aligned.

### 3. StraightTest & StrafeTest

Relatively straight forward. If you follow the steps on the website, everything should work fine besides the strafe(may be troublesome).

THIS IS WHAT THE PREVIOUS YEAR BREBOTICS SAID ABOUT THIS TEST
```bash
StrafeTest, our team failed to tune the robot to strafe straight right/left. We was able to match the distance but the direction was quite messed up.
I believe this was either the problem of the weight distribution or wheel attachment of our robot. 
However, the goal of this process is to match the distance not the heading so if you got the distance right, then you'll be fine.
(+ Heading can manually adjusted while coding the autnomous, so dw)
```
### 4. TrackWidthTuner

For us, this test was realtively quick. Repeat the process about 5 times and use the most accurate value of the five.
AGAIN, The graph is  more important than what you see on the robot(what you see on the robot may be a builder problem so communicate 
with them or else you may waste time trying to fix a hardware issue through code.)

### 5. TurnTest

An error range of 1-3 is what you should be aiming for. 

### 6. FollowerPIDTuner

Back and forth test is recommended for more accuracy "But we couldn't because not enough space"

### 7. Spline Test

The spline test gave us no issues. If the heading is off, redo the TrackWidthTuner and/or TurnTest.
If the distance is off, check your DriveConstants
If the robot is moving completely off route, it's probably a build issue so ask your builders to check to robots
(For us the issue was tight screws on motors)
