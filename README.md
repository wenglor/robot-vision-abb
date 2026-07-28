# Example ABB RAPID program files for the generic vision interface

**Version:** 1.2.0

This repository demonstrates how to use the Generic Vision Interface with wenglor vision devices on an ABB controller. The included `.modx` and `.pgf` files form a working sample program [Generic wenglor vision interface.pgf](sources/Generic%20wenglor%20vision%20interface.pgf) that you can adopt and customize for your application.

> NOTE
>
> This repository focuses exclusively on ABB Robots-specific topics. For general robot vision information, please refer to the [wenglor robot vision manual](https://wenglor.github.io/robot-vision-generic-string/).

📖 **Full documentation** is available in the [online manual](https://wenglor.github.io/robot-vision-abb/)

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Files](#files)
- [Installation](#installation)
- [Running the Sample Program](#running-the-sample-program)
- [Troubleshooting](#troubleshooting)
- [Support & Feedback](#support--feedback)

> NOTE
>
> The generic robot vision API (commands, return values, error codes), the calibration guidelines, and the uniVision job setup are documented once in the [wenglor robot vision manual](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/) and are **not** repeated here. This repository only describes how the ABB example uses them.

---

## Prerequisites

> Tested with OmniCore controller and RobotWare 7.5.13 (minimum required: RobotWare 7.3.2)

- Basic knowledge of **RAPID**
- OmniCore controller (RobotWare 7.3.2+) or IRC5 controller (RobotWare 5.15+) — for IRC5, rename `.modx` files to `.mod`, update references in the `.pgf` file, and activate the **PC Interface** option
- **RapidSockets** enabled in the controller communication configuration (RobotStudio → Communication → Firewall Manager)
- [B60](https://www.wenglor.com/en/Machine-Vision/Smart-Cameras-and-Vision-Sensors/Smart-Camera-B60/c/cxmCID221375) or [Machine Vision Controller (MVC)](https://www.wenglor.com/en/Machine-Vision/Machine-Vision-Controllers/c/cxmCID221381)
- A [uniVision 3](https://www.wenglor.com/en/Machine-Vision/Machine-Vision-Software/Image-Processing-Software-uniVision-3/c/cxmCID222459) job for calibration and object detection, with the robot manufacturer set to **ABB** on the device website (Tab `Jobs` → `Robot Server`)

---

## Files

The [sources](sources) directory of this repository contains:

| File | Contents |
| --- | --- |
| `Generic wenglor vision interface.pgf` | Program file that references the modules below. |
| `wenglorUserConfig.modx` | User configuration (IP, port, poses, jobs, use case). See [User Configuration](docs/2_0_user_configuration/index.md). |
| `wenglorGlobal.modx` | Core and helper functions (socket communication, conversions). |
| `wenglorCalibration.modx` | Hand-eye calibration and verification. |
| `wenglorDetect.modx` | Object detection and movement to detected objects. |

---

## Installation

1. Get the files from the [sources](sources) directory and copy them to the robot controller (e.g. `/HOME` or `/HOME/<project_folder>`).
2. Follow the [user configuration](docs/2_0_user_configuration/index.md) steps.

---

## Running the Sample Program

1. Load the program **Generic wenglor vision interface** on your robot.
2. Select the TCP used for calibration in the FlexPendant.
3. Execute the program and monitor the messages on the FlexPendant display.

For details on the program flow (calibration, single/multi detection, reference frame updates), see [Robot Program](docs/3_0_robot_program/index.md).

---

## Troubleshooting

See the [Troubleshooting](docs/4_0_troubleshooting/index.md) page for insufficient calibration accuracy, height offsets in detected poses, communication errors, device error codes, and unexpected program exits.

---

## Support & Feedback

- **Bugs:** Please open a new Issue in the [GitHub Issues section](https://github.com/wenglor/robot-vision-abb/issues) if needed.
- **Feature Requests & Ideas:** Discuss suggestions in the Discussions → Ideas category under [GitHub Discussions](https://github.com/wenglor/robot-vision-abb/discussions).
- **Product page:** [www.wenglor.com/product/DNNF023](https://www.wenglor.com/product/DNNF023) — uniVision 3 software, device firmware, and operating instructions. The RAPID example files themselves are in this repository's [sources](sources) directory.
