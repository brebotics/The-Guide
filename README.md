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
summary is here:
