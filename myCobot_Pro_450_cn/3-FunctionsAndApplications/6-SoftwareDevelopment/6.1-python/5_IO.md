## IO控制

IO即数据的输入与输出，在我们的机械臂的Basic和Atom上有多个pin脚，这里主要说明末端IO控制夹爪的使用

**案例使用**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500)  # 客户端连接通信

# 打开夹爪
def open_gripper():
    pro450.set_digital_output(1, 0)  # 设置引脚1为低电平
    pro450.set_digital_output(2, 1)  # 设置引脚2为高电平
    time.sleep(0.05)

# 关闭夹爪
def close_gripper():
    pro450.set_digital_output(1, 1)  # 设置引脚1为高电平
    pro450.set_digital_output(2, 0)  # 设置引脚2为低电平
    time.sleep(0.05)

# 夹爪重复开合两次
for i in range(2):
    open_gripper()
    time.sleep(3)
    close_gripper()
```

---

[← 上一章](./4_coord.md) | [下一章 →](./6_gripper.md)