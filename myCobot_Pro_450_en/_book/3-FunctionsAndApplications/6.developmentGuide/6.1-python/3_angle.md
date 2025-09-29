## Joint Control

For serial multi-joint robots, the control of joint space is to control the variables of each joint of the robot, and the goal is to make each joint of the robot reach the target position at a certain speed.

> **Note:** When setting the angle, the limit of different series of robot arms is different. For details, please refer to the parameter introduction of the corresponding model.

**Example Use**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500) # Client connection communication

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