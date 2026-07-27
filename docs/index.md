# ABB Robots Vision Manual

> NOTE
>
> This manual focuses exclusively on ABB Robots-specific topics. For general robot vision information, please refer to the [wenglor robot vision manual](https://wenglor.github.io/robot-vision-generic-string/).

This repository contains an example RAPID program to set up and start the generic vision interface to wenglor Machine Vision Devices on your ABB robot.

The robot vision example for ABB consists of the following files:

- `Generic wenglor vision interface.pgf`
- `wenglorUserConfig.modx`
- `wenglorGlobal.modx`
- `wenglorCalibration.modx`
- `wenglorDetect.modx`

> NOTE
>
> The robot example is available on [www.wenglor.com/product/DNNF023](https://www.wenglor.com/product/DNNF023) → Downloads → Programming examples and configuration files → Examples_Robot_Vision.
>
> - It works for **OmniCore** robot controllers and requires the minimum software version **RobotWare 7.3.2**.
> - To run the examples on **IRC5** robot controllers (minimum software version **RobotWare 5.15**): rename the module files from `.modx` to `.mod`, change the `.modx` references to `.mod` within the PGF file, and activate the option **PC Interface**.

---

## Table of Contents

1. [Installation & Setup](1_0_installation/index.md)
2. [User Configuration](2_0_user_configuration/index.md)
3. [Robot Program](3_0_robot_program/index.md)
4. [Troubleshooting](4_0_troubleshooting/index.md)
5. [Support & Feedback](5_0_support_and_feedback/index.md)

> NOTE
>
> The generic robot vision API (commands, return values, error codes), the calibration guidelines, and the uniVision job setup are documented once in the [wenglor robot vision manual](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/) and are **not** repeated here. This manual only describes how the ABB example uses them.
