# 4. Troubleshooting

Quick reference — jump to the matching symptom below for details:

| Symptom | Likely cause | Section |
| --- | --- | --- |
| Reprojection error is high / picks are inaccurate | Too few or too similar calibration poses, poor calibration plate visibility | [Insufficient calibration accuracy](#insufficient-calibration-accuracy) |
| Robot picks above/below the object | Height offset or wrong tool (TCP) | [Height offset in detected poses](#height-offset-in-detected-poses) |
| No connection / no reply from the camera | Wrong IP/port, RapidSockets disabled, robot server inactive | [Communication errors](#communication-errors) |
| Program shows a warning with a negative number (`-5001` … `-5010`) | Device-side error, e.g. bad job name or missing calibration | [Error codes returned by the device](#error-codes-returned-by-the-device) |
| Program exits without a clear error | Poses not taught, missing detection pose | [Program exits unexpectedly](#program-exits-unexpectedly) |

## Insufficient calibration accuracy

| Check | Action |
| --- | --- |
| Number of calibration poses | Teach more than five (e.g. seven to eleven give more accurate results). Follow the naming scheme and extend the pose sequence in `wenglorCalibration.runCalibration()`. |
| Pose variation | Vary the pose angles as much as possible — motions with non-parallel rotation axes give the most accurate results. |
| Calibration plate visibility | Make sure the plate covers as much of the camera image as possible and is fully visible. |
| Calibration plate type | Prefer the wenglor calibration plate ZVZJ over a printed version — its reprojection error is typically five times smaller. If printing, print the PDF at actual size on flat, stiff material. |
| Reprojection error | Check the value returned by `calibration:calculate`. Typical values are `0.1` for ZVZJ calibration plates and `0.5` for printed ones — higher values indicate a poor calibration. |

## Height offset in detected poses

| Check | Action |
| --- | --- |
| uniVision job | Verify the height offset from the calibration target to the object in **Device Robot Vision** is set properly. |
| Tool (TCP) | Ensure the correct tool is selected — the program reads it via `GetSysData currentToolValue`. |

## Communication errors

| Check | Action |
| --- | --- |
| Device IP/port | Verify that `W_VISION_DEVICE_IP` and `W_VISION_DEVICE_PORT` match the network configuration of the wenglor vision device (default `192.168.100.1`, port `32006`). |
| RapidSockets | In RobotStudio, adjust the network settings of the ABB robot controller for the public network and make sure **RapidSockets** is set to `YES` (Communication → Firewall Manager). |
| Robot server status | Ensure the robot server on the vision device is active (device website → tab `Jobs` → `Robot Server`), with **ABB** selected as the robot manufacturer. |
| Network/firewall | Check general network connectivity and firewall rules between the controller and the device. |

## Error codes returned by the device

If the robot server returns a negative error code (`-5001` … `-5010`), the example maps it to a readable message in `wenglorGlobal.setReturnError` and shows it on the FlexPendant before exiting. For the meaning of each code, see the [Generic Robot Vision Interface → Error codes](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/4_7_0_generic_robot_vision_interface/#error-codes) in the wenglor robot vision manual.

## Program exits unexpectedly

| Symptom | Cause |
| --- | --- |
| Program exits immediately with "calibration poses are not set" | One or more of `wCalibPose1` … `wCalibPose5` is still the empty pose. |
| Program exits with "wDetectionPose pose is not set" | `wDetectionPose` was not taught for the `camera_not_on_robot` use case. |
| Program shows a warning and exits without a clear reason | No reply from the camera, or an unparseable error code. Check the device state via `state[<use_case>];`. |
