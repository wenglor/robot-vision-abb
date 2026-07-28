# ABB Robots Vision Manual

> NOTE
>
> This manual focuses exclusively on ABB Robots-specific topics. For general robot vision information, please refer to the [wenglor robot vision manual](https://wenglor.github.io/robot-vision-generic-string/).

This repository contains an example RAPID program to set up and start the generic vision interface to wenglor Machine Vision Devices on your ABB robot. The program files are available in the [sources](https://github.com/wenglor/robot-vision-abb/tree/main/sources) directory of this repository — see [Installation & Setup](1_0_installation/index.md) for the file list and supported controllers.

> NOTE
>
> Tested with the **OmniCore** controller running **RobotWare 7.5.13** (minimum required: RobotWare 7.3.2). Also supported on **IRC5** controllers (RobotWare 5.15+) — see [Installation & Setup](1_0_installation/index.md) for the additional steps required.

---

## How the manual is organized

```mermaid
graph LR
    A[1. Installation & Setup] --> B[2. User Configuration]
    B --> C[3. Robot Program]
    C -.-> D[4. Troubleshooting]
    D -.-> E[5. Support & Feedback]
```

1. [Installation & Setup](1_0_installation/index.md) — copy the files to the controller, check the supported controller and network requirements, then load the program.
2. [User Configuration](2_0_user_configuration/index.md) — adjust the parameters in `wenglorUserConfig.modx` to your setup.
3. [Robot Program](3_0_robot_program/index.md) — how the RAPID modules implement calibration, detection, and reference-frame updates.
4. [Troubleshooting](4_0_troubleshooting/index.md) — common issues and how to resolve them.
5. [Support & Feedback](5_0_support_and_feedback/index.md) — where to report bugs or suggest features.

> NOTE
>
> The generic robot vision API (commands, return values, error codes), the calibration guidelines, and the uniVision job setup are documented once in the [wenglor robot vision manual](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/) and are **not** repeated here. This manual only describes how the ABB example uses them.
