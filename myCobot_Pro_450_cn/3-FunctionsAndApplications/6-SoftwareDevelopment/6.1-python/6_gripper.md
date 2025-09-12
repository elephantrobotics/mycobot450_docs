## 夹爪控制

使用Python控制夹爪之前，需要先在机械臂上安装连接好夹爪。不同夹爪适配不同的机械臂，这里使用myGripper F100 Pro力控夹爪。

>>注意：使用之前，确保夹爪小屏幕上的通信方式为modbus模式，否则无法正常控制夹爪。参考[ 夹爪屏幕控制](https://docs.elephantrobotics.com/docs/myGripper-F100-cn/5-BasicApplication/5.1.html)

**案例使用**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500)  # 客户端连接通信

print(pro450.get_pro_gripper_firmware_version())  # 读取夹爪主次版本号
time.sleep(1)

print(pro450.get_pro_gripper_angle())  # 读取夹爪角度信息
time.sleep(1)

pro450.set_pro_gripper_angle(50)  # 设置夹爪角度为50
time.sleep(2)

pro450.set_pro_gripper_speed(70)  # 设置夹爪的运行速度为70
time.sleep(1)

pro450.set_pro_gripper_open()  # 设置夹爪全打开
time.sleep(2)

pro450.set_pro_gripper_close()  # 设置夹爪全闭合
time.sleep(2)
```

---

[← 上一章](./5_IO.md) | [下一章 →](./7_exception_description.md)