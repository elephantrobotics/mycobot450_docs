## IO control

IO stands for data input and output. Our robot arm's Basic and Atom pins have multiple pins. This section mainly explains how to use the end-point IO to control the gripper.

**Example Use**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500) # Client connection and communication

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

[← Previous Page](./4_coord.md) | [Next Page →](./6_gripper.md)