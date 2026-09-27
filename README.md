# custom_msgs

ROS 2 interface package with the four messages shared by the M4 firmware, controller and planner: mode command, mode status, aerial trajectory setpoint, and bimodal goal pose.

## Messages

| Message | Content | Topic |
|---|---|---|
| `M4ModeCmd` | requested morphology mode (0 STAND, 1 UAV, 2 CROUCH1, 4 CROUCH2) | `/auto/mode_cmd` |
| `M4ModeStatus` | current configuration, offboard state, AUTO / odometry / arm-pending flags | `/auto/mode_status` |
| `M4TrajectorySetpoint` | aerial position / velocity / acceleration / heading setpoint in the ENU odometry frame | `/auto/trajectory_waypoint` |
| `M4BimodelPose` | goal pose tagged TERRESTRIAL (0) or AERIAL (1) | goal topic of `m4_bimodel_controller` |

## Packages that depend on this package

| Package | Repository | Messages used |
|---|---|---|
| `m4_firmware` | m4-firmware (submodule of m4-firmware-ros2) | `M4ModeCmd`, `M4ModeStatus`, `M4TrajectorySetpoint` |
| `m4_bimodel_controller` | m4_bimodel_controller | `M4ModeCmd`, `M4ModeStatus`, `M4TrajectorySetpoint`, `M4BimodelPose` |
| `m4_local_planner` | m4_local_planner | `M4ModeCmd`, `M4ModeStatus`, `M4TrajectorySetpoint` |

All three declare `<depend>custom_msgs</depend>` and `find_package(custom_msgs REQUIRED)`, so this package must be built (or sourced) before them.
A field change here requires rebuilding all three.

## Build

```bash
colcon build --packages-select custom_msgs
```
