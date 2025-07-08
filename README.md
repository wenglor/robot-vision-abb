# Example ABB RAPID program files for the generic vision interface

**Version:** 1.1.0

This repository demonstrates how to use the Generic Vision Interface with wenglor vision devices on a ABB controller. The included `.modx` and `.pgf` files form a working sample program [Generic wenglor vision interface.modx](sources/Generic%20wenglor%20vision%20interface.pgf) that you can adopt and customize for your application.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Running the Sample Program](#running-the-sample-program)
4. [Configuration (`wenglorUserConfig.modx`)](#configuration-wengloruserconfigmodx)
   1. [Network Setup](#network-setup)
   2. [Adjusting Parameter](#adjusting-parameter)
   3. [Teaching Poses](#teaching-poses-and-defining-movements)
5. [Troubleshooting](#troubleshooting)
   1. [Communication errors](#communication-errors)
   2. [Insufficient Calibration Accuracy](#insufficient-calibration-accuracy)
6. [Support & Feedback](#support--feedback)

---

## Prerequisites

> Tested with OmniCore controller and Robotware 7.5.13

- Basic knowledge of **RAPID**
- Omnicore controller, IRC5 is currently not supported
- RapidSocket are enabled in the controller communication configuration
- [B60](https://www.wenglor.com/de/Machine-Vision/Smart-Cameras-und-Vision-Sensoren/Smart-Camera-B60/c/cxmCID221375) (firmware >= 1.4) or [Machine Vision Controller (MVC)](https://www.wenglor.com/de/Machine-Vision/Machine-Vision-Controller/c/cxmCID221381) (firmware >= 1.1)
- A [uniVision](https://www.wenglor.com/de/Machine-Vision/Machine-Vision-Software/Bildverarbeitungssoftware-uniVision-3/c/cxmCID222459) job for calibration and object detection

---

## Installation

1. Download the files from the [sources](sources) directory.
2. Copy them to the robot controller.

   | Sources                                        | Destination                                      |
   |------------------------------------------------|--------------------------------------------------|
   | robot files from [sources folder](sources)     | `/HOME` or `/HOME/<project_folder>`              |

3. Follow the [configuration](#configuration-wengloruserconfigmodx) steps.

---

## Running the Sample Program

1. Load the program [Generic wenglor vision interface.modx](sources/Generic%20wenglor%20vision%20interface.pgf) on your robot.
2. Select the TCP used for calibration in the FlexPendant.
3. Execute the program and monitor the messages on the FlexPendant display.

---

## Configuration (`wenglorUserConfig.modx`)

There are two options to set the variables:

1. You can either update those values by navigating to the [wenglorUserConfig.modx file](sources/wenglorUserConfig.modx)
2. By using the *Program Data* module and change the scope to the wenglorUserConfig and navigate through the data types

### Network Setup

```modx
    ! Replace ip address and port with your setup
    CONST string WENGLOR_IP_ADDRESS:="192.168.100.1";
    CONST num WENGLOR_CAM_PORT:=32006;
```

### Adjusting Parameter

<details>
   <summary>Click to see the relevant parameter adjustments in the wenglorUserConfig.modx file </summary>

```modx
    ! Replace ip address and port with your setup
    CONST string WENGLOR_IP_ADDRESS:="192.168.100.1";
    CONST num WENGLOR_CAM_PORT:=32006;

    ! Comment out the correct line depending on the selected camera/robot setup
    CONST string WENGLOR_USE_CASE:="camera_on_robot";
    !CONST string WENGLOR_USE_CASE := "camera_not_on_robot";

    ! Replace with the calibration plate you are using
    ! if you are using zvzj005, replace with zvzj001 and
    ! if you are using zvzj006, replace with zvzj002
    CONST string WENGLOR_CALIBRATION_PLATE:="zvzj001";
    ! Replace the calibration job with the one you created in uniVision
    CONST string WENGLOR_CALIBRATION_JOB:="calibration.u3p";
    CONST string WENGLOR_DETECTION_JOB:="find_objects.u3p";

    ! Adjust validation z safety offset [mm]
    CONST num WENGLOR_Z_SAFETY_OFFSET_MM:=10;
```

</details>

### Teaching Poses and Defining Movements

If you taught more than 5 poses remember to update the number of calibration poses

<details>
   <summary>Click to see where to set the poses in the wenglorUserConfig.src file </summary>

```modx
    ! Set speed for calibration movements here
    CONST speeddata WENGLOR_CALIB_SPEED:=v100;
    ! Set calibration poses here
    VAR robtarget wenglorCalib1:=[[0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0,0,0]];
    VAR robtarget wenglorCalib2:=[[0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0,0,0]];
    VAR robtarget wenglorCalib3:=[[0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0,0,0]];
    VAR robtarget wenglorCalib4:=[[0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0,0,0]];
    VAR robtarget wenglorCalib5:=[[0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0,0,0]];

    ! Set wenglorDetection pose here for camera_not_on_robot case, otherwise don't change it as will be changed in runCalibration()
    PERS robtarget wenglorDetection:=[[0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0,0,0]];
```

</details>

## Troubleshooting

### Communication Errors

- Verify IP/port in [wenglorUserConfig.modx](sources/wenglorUserConfig.modx)
- Ensure the robot server on the vision device is active
  - Go to the device website->Jobs->Processing Instance->Robot Server
- Check network connectivity/firewall

### Insufficient Calibration Accuracy

You can use more than 5 calibration poses by adding more calibration movements in the [wenglorCalibration.modx](sources/wenglorCalibration.modx) file.

<details>
   <summary>Click to see where to set the poses in the wenglorUserConfig.src file </summary>

   ```modx
      PROC runCalibration()
         ...      <!-- Non relevant code was cut out -->

        MoveL wenglorCalib1,WENGLOR_CALIB_SPEED,fine,currentToolValue;
        WaitTime 1;
        sendSimpleCommand("calibration:add["+getRobPos()+"];");

        MoveL wenglorCalib2,WENGLOR_CALIB_SPEED,fine,currentToolValue;
        WaitTime 1;
        sendSimpleCommand("calibration:add["+getRobPos()+"];");

        MoveL wenglorCalib3,WENGLOR_CALIB_SPEED,fine,currentToolValue;
        WaitTime 1;
        sendSimpleCommand("calibration:add["+getRobPos()+"];");

        MoveL wenglorCalib4,WENGLOR_CALIB_SPEED,fine,currentToolValue;
        WaitTime 1;
        sendSimpleCommand("calibration:add["+getRobPos()+"];");

        MoveL wenglorCalib5,WENGLOR_CALIB_SPEED,fine,currentToolValue;
        WaitTime 1;
        sendSimpleCommand("calibration:add["+getRobPos()+"];");

        ! Add more calibration poses if wanted                       <!-- Add more calibration poses using the same scheme -->
   ```

</details>

---

## Support & Feedback

- **Bugs:** Please open a new Issue in the [GitHub Issues section](../../issues) if needed
- **Feature Requests & Ideas:** Discuss suggestions in the Discussions → Ideas category under [GitHub Discussions](../../discussions)
