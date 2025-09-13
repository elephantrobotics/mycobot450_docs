## Gripper control

Before using Python to control the gripper, you must first install and connect the gripper to the robotic arm. Different grippers are compatible with different robotic arms. Here, we use the myGripper F100 Pro force-controlled gripper.

>>Note: Before use, ensure that the communication mode on the gripper's small screen is set to Modbus mode; otherwise, the gripper will not function properly. Refer to [Gripper Screen Control](https://docs.elephantrobotics.com/docs/myGripper-F100-en/5-BasicApplication/5.1.html)

**Example Use**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500) # Client connection communication

print(pro450.get_pro_gripper_firmware_version()) # Read the major and minor version numbers of the gripper

time.sleep(1)

print(pro450.get_pro_gripper_angle()) # Read the gripper angle information

time.sleep(1)

pro450.set_pro_gripper_angle(50) # Set the gripper angle to 50
time.sleep(2)

pro450.set_pro_gripper_speed(70) # Set the gripper speed to 70
time.sleep(1)

pro450.set_pro_gripper_open() # Set the gripper to fully open
time.sleep(2)

pro450.set_pro_gripper_close() # Set the gripper to fully close
time.sleep(2)
```

---

[← Previous Page](./5_IO.md) | [Next Page →](./7_exception_description.md)