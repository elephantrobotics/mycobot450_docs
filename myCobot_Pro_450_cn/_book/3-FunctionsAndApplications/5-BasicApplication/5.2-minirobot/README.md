# MiniRobot使用指南

MiniRobot是myCobot Pro 450机械臂的控制面板，提供了丰富的功能接口，方便用户直观地操作和监控机械臂。本文档汇总了MiniRobot的主要功能模块及其使用方法。

## 主要功能模块

### [1.首次使用](./5.2.1-home.md)
机械臂上电后，MiniRobot会显示Logo并进入主界面。主界面默认显示机械臂的关节信息和静态IP信息。通过屏幕底部按键可切换显示不同信息。
在主界面下:
- A键：进入菜单界面（30秒无操作自动返回主界面）
- B键：显示角度信息和静态IP
- C键：显示坐标信息和静态IP
- D键：显示末端M8接口的输入输出状态

### [2.DragTeach](./5.2.2-dragteach.md)
通过直观的拖动操作来录制和播放机械臂运动轨迹：
- Record：录制机械臂运动轨迹（最长120秒）
- Play：播放已保存的轨迹文件
- 支持RAM和Flash两种存储方式
- Flash中保存的轨迹可上传至myStudio Pro的生产文件夹

### [3.BlocklyRunner](./5.2.3-blocklyrunner.md)
管理和执行通过myStudio Pro或MiniRobot发布的轨迹文件：
- 自动检查myStudio Pro的生产文件夹中的已发布轨迹
- 支持播放、暂停、停止操作
- 可设置单次循环或无限循环播放模式，默认无限循环播放
- 支持删除已发布的轨迹文件

### [4.QuickMove](./5.2.4-quickmove.md)
提供机械臂的精确移动控制：
- FreeMove（自由移动）：长按末端按钮可自由拖动机械臂
- JogMove（关节点动）：通过点动控制单个关节运动
- 支持角度模式和坐标模式
- 单步0.1°，长按连续运动

### [5.Calibration](./5.2.5-calibration.md)
用于校准机械臂各关节的零位位置：
- 选择需要校准的关节
- 使用A、B键调整关节位置
- 运动至校准位置后按下C键保存，关节角度将重置为0°

### [6.Firmware](./5.2.6-firmware.md)
显示机械臂的所有版本信息：
- RobotID：机械臂唯一标识符
- Screen：MiniRobot版本
- System：系统版本
- Soft：myStudio Pro版本 + 运动控制版本
- Tool：末端版本

### [7.Connection](./5.2.7-connection.md)
查看机械臂的网络连接信息：
- 可选择不同网络接口
- 显示当前网络配置信息

### [8.Settings](./5.2.8-settings.md)
机械臂的设置选项：
- Pack Stance（打包姿态）：可进行姿态打包
- Clear Error（清除错误）：可清除关节限位（回零）、清除奇异点报错

### [9.Q&A](./5.2.9-Q&A.md)
列出了使用 MiniRobot 控制机械臂时的常见问题及解答。

## 操作注意事项
- 在自由移动模式下，电机制动器会松开，请务必注意安全
- 菜单界面30秒无操作会自动返回主界面
- 录制轨迹有最长时间限制（120秒）
- RAM中保存的轨迹在机器重启后会丢失

## 文件保存说明
- myStudio Pro的生产文件夹：已发布的轨迹文件
- myStudio Pro的测试文件夹：未发布的轨迹文件
- MiniRobot中进行Flash保存会覆盖之前的文件，仅保留最新版本
- MiniRobot中只有保存在Flash中的轨迹文件才可以被上传至myStudio Pro的生产文件夹
- 关于myStudio Pro的生产/测试文件夹的详细介绍可跳转至[5.3.2 myBlockly的文件管理](../5.3-myStudioPro/5.3.2-myBlockly.md#12-文件管理)

## 错误码

机器运动中出现的错误码对照表如下：

### 算法错误

| 错误编码 | 报错名称 | 错误描述 | 解决方案 |
|---------|----------|----------|----------|
| 1-01-1 ~ 1-01-6 | 超出软件限位 | 关节1-6超出软件限位 | **Python**:<br>方案A：使用`over_limit_return_zero`接口回零<br>方案B：使用`set_free_move_mode`接口切换至自由移动模式，放松异常关节，手动移动到限位内<br><br>**MiniRobot**:<br>方案A：切换至FreeMove模式，放松异常关节，手动移动到限位内<br>方案B：切换至JogMove模式，点动控制移动到限位内<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮 |
| 1-32-0 | 坐标无解 | 该坐标无法抵达 | **使用Python**<br>方案A：使用`over_limit_return_zero`接口回零<br>方案B：使用`send_angles`离开当前位置<br><br>**使用MiniRobot**<br>方案A：当触发错误时，小屏幕会提示警告，可使用C按键的回退功能<br><br>**使用myStudio**<br>方案A：登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br>尝试mystdio进行修复：[报警提示](../5.3-myStudioPro/README.md#报警提示)<br><br>**售后**<br>方案A：如以上方案都无法解决请联系售后 |
| 1-33-0 | 直线运动无相邻解 | 直线运动因途经点无法抵达而终止 | 同上 |
| 1-36-0 | 奇异位置无解 | 坐标运动经过奇异位置 | 同上 |
| 1-40-0 | 坐标指令超限 | 坐标指令超出机械臂活动范围 | **MiniRobot**:<br>方案A：切换至快速移动模式，放松异常关节，手动移动到限位内<br>方案B：切换至JogMove模式，点动控制向其他方向移动 |
| 1-49-0 | 辨识精度异常 | 参数辨识失败 | **售后**:<br>联系售后尝试解决，无法解决时寄回排查 |
| 1-81-1 ~ 1-81-6 | 触发碰撞检测 | 关节1-6触发碰撞检测 | **Python**:<br>使用`resume`接口恢复<br><br>**myStudio**:<br>方案A：登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br>方案B：登录webapp → 右上角重新上下电<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |

### 电机错误

| 错误编码 | 报错名称 | 错误描述 | 解决方案 |
|---------|----------|----------|----------|
| 2-01-1 ~ 2-01-6 | CAN总线错误 | CAN总线错误，机器人停止运行 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>方案A：登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br>方案B：登录webapp → 右上角重新上下电<br><br>**其他**:<br>尝试整机重启<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-02-1 ~ 2-02-6 | 短路 | 短路，机器人停止运行 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-03-1 ~ 2-03-6 | 关节接收到无效数据 | 无效的设置数据 | **myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-04-1 ~ 2-04-6 | 控制错误 | 控制错误 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**其他**:<br>检测是否撞到硬件限位、关节放松手动转动是否正常<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-05-1 ~ 2-05-6 | CAN通信错误 | CAN通信错误 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-06-1 ~ 2-06-6 | 电机反馈错误 | 反馈错误 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-07-1 ~ 2-07-6 | 正限位开关激活 | 正限位开关激活 | **myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-08-1 ~ 2-08-6 | 负限位开关激活 | 负限位开关激活 | **myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-09-1 ~ 2-09-6 | 过流 | 过流 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**其他**:<br>检测是否撞到硬件限位、关节放松手动转动是否正常<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-10-1 ~ 2-10-6 | I2t保护 | I2t保护 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**其他**:<br>检测是否撞到硬件限位、关节放松手动转动是否正常<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-11-1 ~ 2-11-6 | 过温 | 过温 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-12-1 ~ 2-12-6 | 驱动板过温 | 驱动板过温 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-13-1 ~ 2-13-6 | 过压 | 过压 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-14-1 ~ 2-14-6 | 欠压 | 欠压 | **Python**:<br>使用`servo_restore`接口异常恢复<br><br>**myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-15-1 ~ 2-15-6 | 命令错误 | 命令错误 | **myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |
| 2-16-1 ~ 2-16-6 | 启用处于非活动状态 | 启用处于非活动状态 | **myStudio**:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br>**售后**:<br>如以上方案都无法解决请联系售后 |

### 软件错误

<table style="width:100%; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">错误编码</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">报错名称</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 30%;">错误描述</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 40%;">解决方案</th>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-01-1 ~ 3-01-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">CAN初始化异常</td>
    <td style="border: 1px solid #ddd; padding: 8px;">CAN初始化异常。表现：机器无法使能、控制等。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>其他（优先）</strong>:<br>1. 查看供电是否正常<br>2. 急停是否拍下<br><br><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-02-1 ~ 3-02-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机初始化异常</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机初始化异常。表现：机器无法正常反馈关节信息、控制等。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>其他（优先）</strong>:<br>1. 查看供电是否正常<br>2. 急停是否拍下<br><br><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-03-1 ~ 3-03-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机发送异常</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机发送异常。表现：机器位置反馈等异常。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>使用`servo_restore`接口异常恢复<br><br><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-04-1 ~ 3-04-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机接收异常</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机接收异常。表现：机器位置反馈等异常。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>使用`servo_restore`接口异常恢复<br><br><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-05-1 ~ 3-05-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">位置超差</td>
    <td style="border: 1px solid #ddd; padding: 8px;">位置超差。表现：机器掉使能，无法运动控制。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>使用`servo_restore`接口异常恢复<br><br><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-06-1 ~ 3-06-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">末端发送异常</td>
    <td style="border: 1px solid #ddd; padding: 8px;">末端发送异常。表现：末端接口反馈异常。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>使用`servo_restore`接口异常恢复<br><br><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-07-1 ~ 3-07-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">末端接收异常</td>
    <td style="border: 1px solid #ddd; padding: 8px;">末端接收异常。表现：末端接口反馈异常。不影响机器运动，影响末端功能（如LED、夹爪）。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>Python</strong>:<br>使用`servo_restore`接口异常恢复<br><br><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-08-1 ~ 3-08-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机编码器报错</td>
    <td style="border: 1px solid #ddd; padding: 8px;">电机编码器报错，编码器报错时不可运动，需要清除编码器报错。旧版电机驱动板无报错（即使报了编码器错误，软件无法反馈异常）。区分新旧：板子上带电池的为新驱动板或联系售后。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">3-09-1 ~ 3-09-6</td>
    <td style="border: 1px solid #ddd; padding: 8px;">掉使能反馈</td>
    <td style="border: 1px solid #ddd; padding: 8px;">掉使能会反馈，运动前机器必须是使能状态。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>myStudio</strong>:<br>登录myStudio → 点击右下角状态栏 → 点击"修复"按钮<br><br><strong>售后</strong>:<br>如以上方案都无法解决请联系售后</td>
  </tr>
</table>

### 通信错误

<table style="width:100%; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">错误编码</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 15%;">报错名称</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 30%;">错误描述</th>
    <th style="border: 1px solid #ddd; padding: 8px; width: 40%;">解决方案</th>
  </tr>
  <tr>
    <td style="border: 1px solid #ddd; padding: 8px;">4-01-0</td>
    <td style="border: 1px solid #ddd; padding: 8px;">后端通信异常</td>
    <td style="border: 1px solid #ddd; padding: 8px;">后端通信异常。表现：机械臂实际运动与操作不符，或者出现机械臂停留在上一步等。</td>
    <td style="border: 1px solid #ddd; padding: 8px;"><strong>方案A</strong>：<br>1. 先关掉闭环失败弹窗<br>2. 重新进行一次操作检查是否还提示闭环失败或者退回主页面检查数据是否变灰色<br>3. 如是启动机器臂即可恢复<br><br><strong>方案B</strong>：<br>1. 可能是处于错误状态，如奇异点或者关节限位<br>2. 前往"setting"-"clear Error"检查是否处于错误状态，需要先清除错误状态再继续操作</td>
  </tr>
</table>

[← 上一章](../5.1-SystemInstructions.md) | [下一章 →](./5.2.1-home.md)