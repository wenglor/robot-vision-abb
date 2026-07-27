# Troubleshooting

## Insufficient calibration accuracy

- Use more than five calibration poses (seven to eleven give better results). Follow the naming scheme and extend the pose sequence in `wenglorCalibration.runCalibration()`.
- Increase the variation between poses — especially in the pose angles. The variance of the calibration *movements* matters more than the variance of the poses.
- Make sure the calibration plate covers as much of the camera image as possible and is fully visible.
- Prefer a wenglor ZVZJ calibration plate over a printed one (typical reprojection error `0.1` vs `0.5`). If printing, print at actual size on stiff, flat material.
- Check the reprojection error returned by `calibration:calculate` — high values indicate a poor calibration.

## Height offset in detected poses

- Check that the uniVision job is set properly, especially the height offset from the calibration target to the object in the **Device Robot Vision**.
- Ensure the correct tool (TCP) is selected — the program reads it via `GetSysData currentToolValue`.

## Communication errors

- Verify that the network configuration of the wenglor vision device matches your setup (default device IP `192.168.100.1`, port `32006`).
- In RobotStudio, make sure **RapidSockets** is set to `YES` (Communication → Firewall Manager) and that the controller is configured for the public network.
- Ensure the robot server on the vision device is active: device website → Jobs → Processing Instance → Robot Server, with **ABB** selected as the robot manufacturer.
- Check general network connectivity and firewall rules between the controller and the device.

## Error codes returned by the device

If the robot server returns a negative error code (`-5001` … `-5010`), the example maps it to a readable message in `wenglorGlobal.setReturnError` and shows it on the FlexPendant before exiting. For the meaning of each code, see the [Generic Robot Vision Interface → Error codes](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/4_5_0_generic_robot_vision_interface/#error-codes) in the wenglor robot vision manual.

## Program exits unexpectedly

- Calibration poses not set: `wCalibPose1` … `wCalibPose5` must not be the empty pose.
- `wDetectionPose` not set for the `camera_not_on_robot` use case.
- No reply from the camera, or an unparseable error code — the program shows a warning and exits. Check the device state via `state[<use_case>];`.
