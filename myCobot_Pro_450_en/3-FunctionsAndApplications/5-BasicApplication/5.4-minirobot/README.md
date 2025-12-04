# MiniRobot User Guide

## Introduction
MiniRobot is the control panel for myCobot Pro 450 robotic arm, providing rich functional interfaces for users to intuitively operate and monitor the robotic arm. This document summarizes the main functional modules of MiniRobot and their usage methods.

## Main Functional Modules

### 1. First-Time Use
After powering on the robotic arm, MiniRobot will display the Logo and enter the main interface. The main interface displays the joint information and static IP information of the robotic arm by default. You can switch to display different information using the buttons at the bottom of the screen:
- Button C: Display coordinate information and static IP
- Button D: Display input/output status of the end M8 interface
- Button A: Enter the menu interface (automatically returns to the main interface after 30 seconds of inactivity)

### 2. DragTeach Function
Record and play robotic arm motion trajectories through intuitive dragging operations:
- Record: Record robotic arm motion trajectories (maximum 120 seconds)
- Play: Play saved trajectory files
- Support for both RAM and Flash storage methods
- Trajectories saved in Flash can be uploaded to the Web production folder

### 3. BlocklyRunner Function
Manage and execute trajectory files published through the Web:
- Automatically check published trajectories in the Web production folder
- Support play, pause, and stop operations
- Single loop or infinite loop playback modes available
- Support for deleting published trajectory files

### 4. QuickMove Function
Provide precise movement control of the robotic arm:
- FreeMove: Long-press the end buttons to freely drag the robotic arm
- JogMove: Control individual joint movement through jogging
  - Support angle mode and coordinate mode
  - Single step 0.1°, continuous movement with long press

### 5. Calibration Function
Used to calibrate the zero position of each joint of the robotic arm:
- Select the joint that needs calibration
- Use buttons A and B to adjust joint position
- After moving to the calibration position, press button C to save, and the joint angle will reset to 0°

### 6. Firmware Function
Display all version information of the robotic arm:
- RobotID: Unique identifier for the robotic arm
- Screen: MiniRobot version
- System: System version
- Soft: Web + Backend + Motion control version
- Tool: End effector version

### 7. Connection Function
View the network connection information of the robotic arm:
- Multiple network interfaces available for selection
- Display current network configuration information

## Operation Notes
- In FreeMove mode, the motor brakes will release, please ensure safety
- The menu interface will automatically return to the main interface after 30 seconds of inactivity
- There is a maximum time limit for recording trajectories (120 seconds)
- Trajectories saved in RAM will be lost after machine restart

## File Saving Instructions
- Web production folder: Published trajectory files
- Web test folder: Unpublished trajectory files
- Flash saving will overwrite previous files, only the latest version is retained