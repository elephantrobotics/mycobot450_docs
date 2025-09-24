## IO控制
IO即数据的输入与输出，在我们的机械臂的Basic和Atom上有多个pin脚，通过以下函数接口可以对其设置其输入输出模式。

* **myCobot：**

<img src="../../../resources\3-FunctionsAndApplications\6.developmentGuide\python\io/mycobotIO.jpg" style="zoom: 67%;" />


### 末端 IO 控制

#### `set_digital_output(pin_no, pin_signal)`

- **功能:** 设置末端IO状态
- **参数**
  - `pin_no` (int): 引脚号，范围 1 ~ 2
  - `pin_signal` (int): 0 / 1, 0 - 低电平，1 - 高电平
- **返回值:**
  - `1`: 完成

#### `get_digital_input(pin_no)`

- **功能:** 获取末端IO状态
- **参数**: `pin_no` (int)，范围 1 ~ 2
- **返回值**: `int` 0 / 1, 0 - 低电平，1 - 高电平


### 底部 IO 控制

#### `set_base_io_output(pin_no, pin_signal)`

- **功能**：设置底部IO输出状态
- **参数**：
  - `pin_no` (`int`) 引脚号，范围 1 ~ 12
  - `pin_signal` (`int`): 0 - 低电平. 1 - 高电平

#### `get_base_io_output(pin_no)`

- **功能：** 获取底部IO输入状态
- **参数:**
  - `pin_no` (`int`) 引脚号，范围 1 ~ 12
- **返回值:** 0 - 低电平. 1 - 高电平 
### 案例使用



---

[← 上一章](./4_coord.md) | [下一章 →](./6_gripper.md)