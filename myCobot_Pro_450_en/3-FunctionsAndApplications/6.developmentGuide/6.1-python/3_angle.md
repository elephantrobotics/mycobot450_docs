## Preparing for Use

Before using the Python API, please ensure that the following hardware and environment are complete:

- **Hardware**
  - MyCobot Pro 450 robot arm
  - Network cable (for connecting the robot arm to the computer)
  - Power adapter
  - Emergency stop switch (for safe operation)

- **Software and Environment**
  - Python 3.6 or later installed
  - The `pymycobot` library installed (using the `pip install pymycobot` terminal command)
  - Ensure that the MyCobot Pro 450 is properly powered on and in standby mode
  - Ensure that the MyCobot Pro 450 server is started

- **Network Configuration**
  - MyCobot Pro 450 default IP address: `192.168.0.232`
  - Default port number: `4500`
  - **Note**: The PC network card IP address must be set to **Same network segment** (e.g., `192.168.0.xxx`, where `xxx` is any number between 2 and 254 and cannot conflict with the robot arm's IP address).
  - Example:
    - Robot arm IP: `192.168.0.232`
    - PC IP: `192.168.0.100`
    - Subnet mask: `255.255.255.0`

---

## Joint Control

For serial multi-joint robots, the control of joint space is to control the variables of each joint of the robot, and the goal is to make each joint of the robot reach the target position at a certain speed.

> **Note:** When setting the angle, the limit of different series of robot arms is different. For details, please refer to the parameter introduction of the corresponding model.

**Example Use**

```python
import time
from pymycobot import Pro450Client

# The default IP address is "192.168.0.232" and the default port number is 4500
pro450 = Pro450Client('192.168.0.232', 4500) # Client connection communication

if pro450.is_power_on() !=1:
    pro450.power_on()  # Power on

print(pro450.get_angles()) # Read all joint angle information

pro450.send_angles([0, 0, 0, 0, 0, 0], 50) # Send all joint angles, speed is 50, so that all joints of the robot arm move to zero position

time.sleep(3)

pro450.send_angle(1, 90, 50) # Send single joint angle, speed is 50, so that J1 joint moves to 90 degrees

time.sleep(2)

pro450.send_angles([0, -10, -123, 45, 0, 90], 50) # Send all joint angles, speed 50
time.sleep(3)
```

---

[← Previous Chapter](./2_API.md) | [Next Chapter→](./4_coord.md)