## 使用前准备

在使用 Python API 之前，请先确认以下硬件和环境准备齐全：

- **硬件设备**  
  - MyCobot Pro 450 机械臂  
  - 网线（用于连接机械臂与电脑）  
  - 电源适配器  
  - 急停开关（确保安全操作）

- **软件与环境**  
  - 已安装 Python 3.6 及以上版本  
  - 已安装 `pymycobot` 库（通过 `pip install pymycobot` 终端命令安装）  
  - 确保 MyCobot Pro 450 已正确上电，并且处于待机状态  
  - 确保 MyCobot Pro 450 的服务端已启动  

- **网络配置**  
  - MyCobot Pro 450 默认 IP 地址：`192.168.0.232`  
  - 默认端口号：`4500`  
  - **注意**：PC 端需要将本机网卡 IP 设置为 **同一网段**（例如 `192.168.0.xxx`，`xxx` 为 2~254 之间的任意数，且不能与机械臂冲突）。  
  - 示例：  
    - 机械臂 IP：`192.168.0.232`  
    - PC IP：`192.168.0.100`  
    - 子网掩码：`255.255.255.0`

---

## IO控制

IO即数据的输入与输出，在我们的机械臂的Basic和Atom上有多个pin脚，这里主要说明末端IO控制夹爪的使用

**案例使用**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500)  # 客户端连接通信

if pro450.is_power_on() !=1:
    pro450.power_on()  # 上电

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

[← 上一页](./4_coord.md) | [下一页 →](./6_gripper.md)