## 夹爪控制

使用Python控制夹爪之前，需要先在机械臂上安装连接好夹爪。不同夹爪适配不同的机械臂（具体适配信息请参考**产品配件**。

> **注意：**
>
> MyCobot 280自适应夹爪将夹爪插在Atom上面的引脚上，具体看下图：
>
> <img src="../../../resources\3-FunctionsAndApplications\6.developmentGuide\python\Jaw/夹爪1.jpg" style="zoom: 67%;" />
>


### 夹爪控制

#### `get_pro_gripper_firmware_version( gripper_id=14)`

- **功能**：读取Pro力控夹爪固件主次版本号
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。

- **返回值**: (`float`) 版本号, x.x

#### `get_pro_gripper_firmware_modified_version(gripper_id=14)`

- **功能**：读取Pro力控夹爪固件修正版本号
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。

- **返回值**：(`int`) 修正版本号

#### `set_pro_gripper_id(target_id, gripper_id=14)`

- **功能**：设置力控夹爪ID。
- **参数**：
  - `target_id` (`int`): 范围1 ~ 254。
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功
  
#### `get_pro_gripper_id(gripper_id=14)`

- **功能**：读取力控夹爪ID。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：`int` 范围1 ~ 254。

#### `set_pro_gripper_angle(gripper_angle, gripper_id=14)`

- **功能**：设置力控夹爪角度。
- **参数**：
  - `gripper_angle` (`int`): 夹爪角度，取值范围 0 ~ 100。
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功
  
#### `get_pro_gripper_angle(gripper_id=14)`

- **功能**：读取力控夹爪角度。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：`int` 0 ~ 100

#### `set_pro_gripper_open(gripper_id=14)`

- **功能**：打开力控夹爪。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `set_pro_gripper_close(gripper_id=14)`

- **功能**：关闭力控夹爪。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `set_pro_gripper_calibration(gripper_id=14)`

- **功能**：设置力控夹爪零位。（首次使用需要先设置零位）
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `get_pro_gripper_status(gripper_id=14)`

- **功能**：读取力控夹爪夹持状态。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值:**
  - `0` - 正在运动。
  - `1` - 停止运动，未检测到夹到物体。
  - `2` - 停止运动，检测到夹到物体。
  - `3` - 检测到夹到物体之后，物体掉落。

#### `set_pro_gripper_enabled(state, gripper_id=14)`

- **功能**：设置力控夹爪使能状态。
- **参数**：
  - `state` (`bool`) ：0 或者1， 0 - 掉使能 1 - 上使能
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `set_pro_gripper_torque(torque_value, gripper_id=14)`

- **功能**：设置力控夹爪扭矩。
- **参数**：
  - `torque_value` (`int`) ：扭矩值，取值范围 0 ~ 100。
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `get_pro_gripper_torque(gripper_id=14)`

- **功能**：读取力控夹爪扭矩。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值:** (`int`) 0 ~ 100

#### `set_pro_gripper_speed(speed, gripper_id=14)`

- **功能**：设置力控夹爪速度。
- **参数**：
  - `speed` (int): 夹爪运动速度，取值范围 1 ~ 100。
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `get_pro_gripper_speed(gripper_id=14)`

- **功能**：读取力控夹爪速度。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：夹爪默认运动速度，范围 1 ~ 100。

#### `set_pro_gripper_abs_angle(gripper_angle, gripper_id=14)`

- **功能**：设置力控夹爪绝对角度。
- **参数**：
  - `gripper_angle` (`int`): 夹爪角度，取值范围 0 ~ 100。
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `set_pro_gripper_io_open_angle(gripper_angle, gripper_id=14)`

- **功能**：设置力控夹爪IO张开角度。
- **参数**：
  - `gripper_angle` (`int`): 夹爪角度，取值范围 0 ~ 100。
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `get_pro_gripper_io_open_angle(gripper_id=14)`

- **功能**：读取力控夹爪IO张开角度。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：`int` 0 ~ 100

#### `set_pro_gripper_io_close_angle(gripper_angle, gripper_id=14)`

- **功能**：设置力控夹爪IO闭合角度。
- **参数**：
  - `gripper_angle` (`int`): 夹爪角度，取值范围 0 ~ 100。
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `get_pro_gripper_io_close_angle(gripper_id=14)`

- **功能**：读取力控夹爪IO闭合角度。
- **参数**：
  - `gripper_id` (`int`): 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：`int` 0 ~ 100

#### `set_pro_gripper_mini_pressure(pressure_value, gripper_id=14)`

- **功能**：设置力控夹爪最小启动力
- **参数**：
  - `pressure_value` (`int`): 启动力值，范围 0 ~ 254。
  - `gripper_id` (`int`) 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `get_pro_gripper_mini_pressure(gripper_id=14)`

- **功能**：读取力控夹爪最小启动力
- **参数**：
  - `gripper_id` (`int`) 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：(`int`) 启动力值，范围 0 ~ 254。

#### `set_pro_gripper_protection_current(current_value, gripper_id=14)`

- **功能**：设置力控夹爪夹持电流
- **参数**：
  - `current_value` (`int`): 夹持电流值，范围 100 ~ 300。
  - `gripper_id` (`int`) 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：
  - 0 - 失败
  - 1 - 成功

#### `get_pro_gripper_protection_current(gripper_id=14)`

- **功能**：读取力控夹爪夹持电流
- **参数**：
  - `gripper_id` (`int`) 夹爪ID，默认14，取值范围 1 ~ 254。
- **返回值**：(`int`) 夹持电流值，范围 100 ~ 300。

### 案例


---

[← 上一章](./5_IO.md) | [下一章 →](./7_example.md)