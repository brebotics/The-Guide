# The Guide
Become Not Stupid™

wuz gud guyz, its ya boy

## Setting up Android Studio
head ova to da [android studio website](https://developer.android.com/studio), n download da exe

make sure ur not on a firewalled wifi connection, gradle issues may occur

now that android studio is installed, download [roadrunner from da github](https://github.com/acmerobotics/road-runner)

open the project with AS(android studio)

## Previous Projects
if your team has existed. copy the code

specifally, their teleop & autonomous files. 

also make sure to update versions so that control hub & robot controller are the same version

## TeleOp
copy da files either from previous year or [INPUT ORIGIN HERE](chrome://dino/)

make sure to UPDATE the variables to ur current build: if the robot has 4 wheels or 6 wheels, if the robot has a claw or a shooter, and make sure that **you have x & y variables to move
ex: basic DriveTrain code
```
package org.firstinspires.ftc.teamcode;

import ...

@TeleOp(name = "ProvTele")
public class ProvTele extends LinearOpMode {
double x;
double y;
double rx;
```
...
```
public void runOpMode() {
y = gamepad1.left_stick_y;
x = -gamepad1.left_stick_x * 1.1;
rx = -gamepad1.right_stick_x;
if (opModeIsActive()) {
    while (opModeIsActive()) {
Left_Front.setPower((y + x + rx) * constant);
Left_Rear.setPower((y - x + rx) * constant);
Right_Front.setPower((y - x - rx) * constant);
Right_Rear.setPower((y + x - rx) * constant);
...
    }
}
```


## Autonomous
after encountering NO ERRORS, copy the ConceptTensorFlowObjectDetectionWebcam.java from *FtcRobotController/java/.../external/samples* into *TeamCode/java/.../teamcode/*
(using the tfodWebcam file, cuz i assume you wanna learn object detection aswell) (the comments IN the file show you the basics of object detection)

under the **while (opModeIsActive())** bracket, ***AFTER*** the **if statement** put in your code. this can be as simple as motor.forward(10) or full autonomous code.

