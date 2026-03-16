# MiniRobot User Guide

MiniRobot is the control panel for the myCobot Pro 450 robotic arm, providing a rich set of functional interfaces for easy and intuitive operation and monitoring. This document summarizes the main functional modules of MiniRobot and their usage methods.

## Main Functional Modules

### [1.First Use](./5.4.1-home.md) 
After the robotic arm is powered on, MiniRobot will display its logo and enter the main interface. The main interface displays the robotic arm's joint information and static IP information by default. Different information can be switched using the buttons at the bottom of the screen:

On the main interface:

- A button: Enter the menu interface (automatically returns to the main interface after 30 seconds of inactivity)
- B button: Display angle information and static IP
- C button: Display coordinate information and static IP
- D button: Display the input/output status of the M8 interface at the end

### [2.DragTeach](./5.4.2-dragteach.md) 
Record and play back the robotic arm's motion trajectory using intuitive drag-and-drop operations:

- Record: Record the robotic arm's motion trajectory (maximum 120 seconds)
- Play: Play back a saved trajectory file
- Supports both RAM and Flash storage methods
- Trajectories saved in Flash can be uploaded to the myStudio Pro production folder

### [3.BlocklyRunner](./5.4.3-blocklyrunner.md) 
Manage and execute trajectory files published by myStudio Pro or MiniRobot:

- Automatically checks published trajectories in the myStudio Pro production folder
- Supports play, pause, and stop operations
- Sets single-loop or infinite loop playback mode, default is infinite loop playback
- Supports deleting published track files

### [4.QuickMove](./5.4.4-quickmove.md) 
Provides precise movement control for the robotic arm:

- FreeMove: Press and hold the end effector button to drag the robotic arm freely
- JogMove: Controls the movement of a single joint by jogging
- Supports angle and coordinate modes
- 0.1° single step, long press for continuous movement

### [5.Calibration](./5.4.5-calibration.md) 
Used to calibrate the zero position of each joint of the robotic arm:

- Select the joint to be calibrated
- Use the A and B keys to adjust the joint position
- After moving to the calibration position, press the C key to save; the joint angle will be reset to 0°

### [6.Firmware](./5.4.6-firmware.md) 
Displays all version information of the robotic arm:

- RobotID: Unique identifier for the robotic arm
- Screen: MiniRobot version
- System: System version
- Soft: myStudio Pro version + Motion Control version
- Tool: End-effector version

### [7.Connection](./5.4.7-connection.md) 
View the robotic arm's network connection information:

- Select different network interfaces
- Display current network configuration information

### [8.Settings](./5.2.8-settings.md) 
Setting options for the robotic arm:

- Pack Stance: Can perform posture packing
- Clear Error: Can clear joint limit (return to zero) and clear singularity error

### [9.Q&A](./5.2.9-Q&A.md) 
Lists common questions and answers about using MiniRobot to control the robotic arm.

## Operation Precautions

- In free movement mode, the motor brake will release; please be careful.
- The menu interface will automatically return to the main interface after 30 seconds of inactivity.
- There is a maximum recording time limit (120 seconds).
- Tracks saved in RAM will be lost after a machine restart.

## File Saving Instructions

- myStudio Pro production folder: Published track files
- myStudio Pro test folder: Unpublished track files
- Saving to Flash in MiniRobot will overwrite previous files, keeping only the latest version
- Only track files saved in Flash in MiniRobot can be uploaded to the myStudio Pro production folder
- For detailed introduction of myStudio Pro production/test folders, you can jump to [5.3.2 myBlockly File Management](../5.3-myStudioPro/5.3.2-myBlockly.md#12-file-management)


## Error Codes

Error codes that occur during machine operation are divided into algorithm error codes, motor error codes, software error codes, and communication error codes. The error code table is as follows:

### Algorithm Error

| Error Code | Error Name | Error Description | Solution |
|-----------|-----------|-----------------|---------|
| 1-01-1 ~ 1-01-6 | Joint proximity limit | Joint 1-6 beyond software limit | **Python**:<br>Option A: Use `over_limit_return_zero` interface to return to zero<br>Option B: Use `set_free_move_mode` interface to switch to free movement mode, release the abnormal joint, and manually move it to the limit<br><br>**MiniRobot**:<br>Option A: Switch to FreeMove mode, release the abnormal joint, and manually move it to the limit<br>Option B: Switch to JogMove mode, and move it to the limit by jogging<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button |
| 1-32-0 | Coord have no solution | The coordinate cannot be reached | **Using Python**<br>Option A: Use `over_limit_return_zero` interface to return to zero<br>Option B: Use `send_angles` to leave the current position<br><br>**Using MiniRobot**<br>Option A: When an error is triggered, the small screen will display a warning, and you can use the C button to retreat<br><br>**Using myStudio**<br>Option A: Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br>Try myStudio for repair: [Alarm Notification](../5.3-myStudioPro/README.md#alarm-notification)<br><br>**After-sales**<br>Option A: If the above solutions cannot solve the problem, please contact after-sales |
| 1-33-0 | Straight-line motion has no adjacent solution | Straight-line motion terminates because the passing point cannot be reached | Same as above |
| 1-36-0 | Singular position is unsolvable | Coordinate movement passes through a singular position | Same as above |
| 1-40-0 | Coord proximity limit | Coordinate command exceeds the robotic arm's range of motion | **MiniRobot**:<br>Option A: Switch to quick movement mode, release the abnormal joint, and manually move it to the limit<br>Option B: Switch to JogMove mode, and move it in other directions by jogging |
| 1-49-0 | Recognition accuracy anomaly | Parameter identification failed | **After-sales**<br>Contact after-sales to try to solve the problem, and send it back for inspection if it cannot be solved |
| 1-81-1 ~ 1-81-6 | Trigger collision detection | Joint 1-6 triggers collision detection | **Python**:<br>Use `resume` interface to recover<br><br>**myStudio**:<br>Option A: Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br>Option B: Login to webapp → power on/off again at the top right corner<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |

### Motor Error

| Error Code | Error Name | Error Description | Solution |
|-----------|-----------|-----------------|---------|
| 2-01-1 ~ 2-01-6 | CAN bus error, Robot has stopped operating | CAN bus error, robot stops running | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Option A: Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br>Option B: Login to webapp → power on/off again at the top right corner<br><br>**Other**:<br>Try restarting the entire machine<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-02-1 ~ 2-02-6 | Short Circuit | Short circuit, robot stops running | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-03-1 ~ 2-03-6 | Joint received invalid data | Invalid setting data | **myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-04-1 ~ 2-04-6 | Control error | Control error | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**Other**:<br>Check if it hits the hardware limit, and if the joint can rotate normally when released<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-05-1 ~ 2-05-6 | CAN communication error | CAN communication error | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-06-1 ~ 2-06-6 | Motor feedback error | Feedback error | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-07-1 ~ 2-07-6 | Positive limit switch activated | Positive limit switch activated | **myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-08-1 ~ 2-08-6 | Negative limit switch activated | Negative limit switch activated | **myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-09-1 ~ 2-09-6 | Over current | Over current | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**Other**:<br>Check if it hits the hardware limit, and if the joint can rotate normally when released<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-10-1 ~ 2-10-6 | I2t protection | I2t protection | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**Other**:<br>Check if it hits the hardware limit, and if the joint can rotate normally when released<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-11-1 ~ 2-11-6 | Overheating | Overheating | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-12-1 ~ 2-12-6 | Driver board overheating | Driver board overheating | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-13-1 ~ 2-13-6 | Over voltage | Over voltage | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-14-1 ~ 2-14-6 | Under voltage | Under voltage | **Python**:<br>Use `servo_restore` interface for exception recovery<br><br>**myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-15-1 ~ 2-15-6 | Command error | Command error | **myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |
| 2-16-1 ~ 2-16-6 | Enabled in an inactive state | Enabled in an inactive state | **myStudio**:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br>**After-sales**<br>If the above solutions cannot solve the problem, please contact after-sales |

### Software Error

<table style="width:100%; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">Error Code</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">Error Name</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 30%;">Error Description</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 40%;">Solution</th>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-01-1 ~ 3-01-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">CAN initialization exception</td>
    <td style="border: 1px solid #ddd; padding: 8px;">CAN initialization exception. Symptoms: The machine cannot be enabled or controlled.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Other (Priority)</strong>:<br>1. Check if the power supply is normal<br>2. Check if the emergency stop is pressed<br><br><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-02-1 ~ 3-02-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor initialization abnormality</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor initialization abnormality. Symptoms: The machine cannot properly feed back joint information or control.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Other (Priority)</strong>:<br>1. Check if the power supply is normal<br>2. Check if the emergency stop is pressed<br><br><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-03-1 ~ 3-03-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor sending abnormality</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor sending abnormality. Symptoms: Abnormal machine position feedback, etc.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>Use `servo_restore` interface for exception recovery<br><br><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-04-1 ~ 3-04-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor reception abnormality</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor reception abnormality. Symptoms: Abnormal machine position feedback, etc.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>Use `servo_restore` interface for exception recovery<br><br><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-05-1 ~ 3-05-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Location out of tolerance</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Position out of tolerance. Symptoms: The machine loses enable and cannot move and control.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>Use `servo_restore` interface for exception recovery<br><br><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-06-1 ~ 3-06-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">End send exception</td>
    <td style="border: 1px solid #ddd; padding: 8px;">End send exception. Symptoms: Abnormal feedback from the end interface.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>Use `servo_restore` interface for exception recovery<br><br><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-07-1 ~ 3-07-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Terminal receiving exception</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Terminal receiving exception. Symptoms: Abnormal feedback from the end interface. Does not affect machine movement, but affects end functions (such as LED, gripper).</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>Use `servo_restore` interface for exception recovery<br><br><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-08-1 ~ 3-08-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor encoder error</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Motor encoder error. The motor cannot move when the encoder is error. Old motor driver boards have no error reporting (even if an encoder error is reported, the software cannot feedback the exception). To distinguish between old and new: boards with batteries are new driver boards or contact after-sales.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-09-1 ~ 3-09-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Disconnect enable feedback</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Disconnect enable will feedback, the machine must be in enable state before movement.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>myStudio</strong>:<br>Login to myStudio → click the status bar at the bottom right corner → click the "Repair" button<br><br><strong>After-sales</strong><br>If the above solutions cannot solve the problem, please contact after-sales</td>
  </tr>
</table>

### Communication Error

<table style="width:100%; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">Error Code</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">Error Name</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 30%;">Error Description</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 40%;">Solution</th>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">4-01-0</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Backend communication exception</td>
    <td style="border: 1px solid #ddd; padding: 8px;">Backend communication exception. Symptoms: The actual movement of the robotic arm does not match the operation, or the robotic arm stays at the previous step, etc.</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Option A</strong>:<br>1. First close the closed-loop failure pop-up<br>2. Reperform the operation to check if it still prompts closed-loop failure or return to the main page to check if the data turns gray<br>3. If yes, start the robotic arm to recover<br><br><strong>Option B</strong>:<br>1. It may be in an error state, such as singularity or joint limit<br>2. Go to "setting"-"clear Error" to check if it is in an error state, you need to clear the error state first before continuing operation</td>
  </tr>
</table>

---

[← Previous Chapter](../5.1-SystemInstructions.md) | [Next Chapter →](./5.2.1-home.md)
