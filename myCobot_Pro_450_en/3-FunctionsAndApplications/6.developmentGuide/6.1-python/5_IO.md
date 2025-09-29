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

## IO control

IO stands for data input and output. Our robot arm's Basic and Atom pins have multiple pins. This section mainly explains how to use the end-point IO to control the gripper.

**Example Use**

```python
import time
from pymycobot import Pro450Client

# The default IP address is "192.168.0.232" and the default port number is 4500
pro450 = Pro450Client('192.168.0.232', 4500) # Client connection and communication

if pro450.is_power_on() !=1:
    pro450.power_on()  # Power on

# Open the gripper
def open_gripper():
    pro450.set_digital_output(1, 0) # Set pin 1 to a low level
    pro450.set_digital_output(2, 1) # Set pin 2 to a high level
    time.sleep(0.05)

# Close the gripper
def close_gripper():
    pro450.set_digital_output(1, 1) # Set pin 1 to a high level
    pro450.set_digital_output(2, 0) # Set pin 2 to a low level
    time.sleep(0.05)

# Repeat the gripper opening and closing twice
for i in range(2):
    open_gripper()
    time.sleep(3)
    close_gripper()
```
---

[← Previous Chapter](./4_coord.md) | [Next Chapter→](./6_gripper.md)