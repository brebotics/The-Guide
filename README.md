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
 
 ## Object Detection(Vuforia TfLite)
 ```
 OFFICIAL FTC VERSION GUIDE: https://ftc-docs.firstinspires.org/en/latest/ftc_ml/
 ```
 
### Vuforia
1. Make an account and log into vuforia to make your key https://developer.vuforia.com/ 
2. Get [sample](https://github.com/FIRST-Tech-Challenge/FtcRobotController/blob/master/FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples/ConceptTensorFlowObjectDetectionWebcam.java) code for object detection ftc and paste vuforia key 

### Prep
3. Look at competition and determine what you need to detect
4. Create footage (30s long) of the object preferably using low fps(15-30 worked for us)
ftc-ml
5. Log into ftc machine learning(IMPORTANT: you need to use a teacher or mentor’s account or they have to give permission) 
https://ftc-ml.firstinspires.org/ 
6. Upload the footage to the website
7. Click on the blue text, to open the window for tagging objects
8. Create a box around the object, and advance a frame
9 . After 10 frames, use the “Start Tracking” button
10. If a new element is introduced, stop the tracking & repeat steps 8&9
11. Once the video are fully labeled, review the frames to find errors
12. Repeat steps if you want to use multiple videos in 1 dataset

### Datasets
13. Select the videos in ftc-ml homepage & click the produce datasets
14. Review how many labels there are - if there are more/less than expected, relabel the video/s
15. Select the data set & click start training
16. Calculate # of steps using the equation in da guide
17. Once finish you can download da file

### Androidstudio
Take the file - put in da assets folder (FTCRobotController/assets → paste tflite into here)
Go back to ur edited sample code & paste the file’s name into TFOD_MODEL_ASSET
Add the labels of ur objects

```
private static final String TFOD_MODEL_ASSET = "model_20221202_164154.tflite";
    private static final String[] LABELS = {
            "blue",//1
            "purple",//2
            "yellow"//3
    };
```

Make sure you have initVuforia() and initTfod() in your code, as well as the camera activation 

```
 private void initVuforia() {
        VuforiaLocalizer.Parameters parameters = new VuforiaLocalizer.Parameters();

        parameters.vuforiaLicenseKey = VUFORIA_KEY;
        parameters.cameraName = hardwareMap.get(WebcamName.class, "Webcam");

        vuforia = ClassFactory.getInstance().createVuforia(parameters);
    }//end initVuforia()
```
After initializing the code, go to the if(while()) loop
paste in `List<Recognition> updatedRecognitions = tfod.getUpdatedRecognitions();` (make sure “tfod” is your TFObjectDetector object)
  
```
     List<Recognition> updatedRecognitions = tfod.getUpdatedRecognitions();
                if (signal == 0) {
                    for (int i = 0; i < updatedRecognitions.size(); i++) {
                        if (updatedRecognitions.get(i).getLabel().equals("blue")) {
                            signal = 1;
                            telemetry.addData("Signal: ", "blue");
                            break;
                        } else if (updatedRecognitions.get(i).getLabel().equals("purple")) {
                            signal = 2;
                            telemetry.addData("Signal: ", "purple");
                            break;
                        } else if (updatedRecognitions.get(i).getLabel().equals("yellow")) {
                            signal = 3;
                            telemetry.addData("Signal: ", "yellow");
                            break;
                        }
                    telemetry.addData("Signal: ", "none");
                    }
                    telemetry.update();
                }
```
(this code detects an icon, and saves which icon was detected in the var signal)

### Confidence

Found in the initTfod() method, the var `tfodParameters.minResultConfidence` takes a percentage as a float. Adjust this variable as needed to reliably detect the object
