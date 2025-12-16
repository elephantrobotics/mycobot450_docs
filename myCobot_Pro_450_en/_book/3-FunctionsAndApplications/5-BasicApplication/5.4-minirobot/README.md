# MiniRobot User Guide

MiniRobot is the control panel for the myCobot Pro 450 robotic arm, providing a rich set of functional interfaces for easy and intuitive operation and monitoring. This document summarizes the main functional modules of MiniRobot and their usage methods.

## Main Functional Modules

### 1. [First Use](./5.4.1-home.md) 
After the robotic arm is powered on, MiniRobot will display its logo and enter the main interface. The main interface displays the robotic arm's joint information and static IP information by default. Different information can be switched using the buttons at the bottom of the screen:

- C key: Displays coordinate information and static IP

- D key: Displays the input/output status of the M8 interface at the end

- A key: Enters the menu interface (automatically returns to the main interface after 30 seconds of inactivity)

### 2. [DragTeach](./5.4.2-dragteach.md) 
Record and play back robotic arm motion trajectories using intuitive drag-and-drop operations:

- Record: Records robotic arm motion trajectories (maximum 120 seconds)

- Play: Plays saved trajectory files

- Supports both RAM and Flash storage methods

- Trajectories saved in Flash can be uploaded to the myStudio Pro production folder

### 3. [BlocklyRunner](./5.4.3-blocklyrunner.md) 
Manage and execute trajectory files published through myStudio Pro:

- Automatically checks published trajectories in the myStudio Pro production folder

- Supports play, pause, and stop operations

- Can be set to single loop or infinite loop playback mode

Supports deleting published trajectory files

### 4. [QuickMove](./5.4.4-quickmove.md) 
Provides precise movement control for the robotic arm:

- FreeMove: Press and hold the end effector button to freely drag the robotic arm.

- JogMove: Control the movement of a single joint by jogging.

- Supports angle mode and coordinate mode.

- Single step 0.1°, long press for continuous movement.

### 5. [Calibration](./5.4.5-calibration.md) 
Used to calibrate the zero position of each joint of the robotic arm:

- Select the joint to be calibrated.

- Use the A and B keys to adjust the joint position.

- After moving to the calibration position, press the C key to save; the joint angle will be reset to 0°.

### 6. [Firmware](./5.4.6-firmware.md) 
Displays all version information of the robotic arm:

- RobotID: Unique identifier for the robotic arm.

- Screen: MiniRobot version.

- System: System version.

- Soft: myStudio Pro version. Motion Control Version

- Tool: End Version

### 7. [Connection](./5.4.7-connection.md)
View the robotic arm's network connection information:

- Select different network interfaces

- Display current network configuration information

## Operation Precautions

- In free movement mode, the motor brake will release; please be extremely careful.

- The menu interface will automatically return to the main interface after 30 seconds of inactivity.

- There is a maximum recording time limit (120 seconds).

- Tracks saved in RAM will be lost after a machine restart.

## File Saving Instructions

- myStudio Pro production folder: Published track files

- myStudio Pro test folder: Unpublished track files

- Flash saving will overwrite previous files; only the latest version will be retained.