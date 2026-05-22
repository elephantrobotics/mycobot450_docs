# C++（RobotDriver / MyCobotPro450）

**使用 C++ 与本公司 RobotDriver 工程**（`RobotArm` 等），可在 **Linux** 下进行二次开发，完成关节控制、坐标控制及与主控的 TCP 通信等。适用于 **MyCobotPro450**；夹爪、底部/末端 IO 等能力以 Python 或其它客户端为准时，请参阅对应说明。

![pic](../../../resources/3-FunctionsAndApplications/6.developmentGuide/Cplus/Cplus.jpg)

## C++是什么？

C++是C语言的继承，它既可以进行C语言的过程化程序设计，又可以进行以抽象数据类型为特点的基于对象的程序设计，还可以进行以继承和多态为特点的面向对象的程序设计。<br>
C++擅长面向对象程序设计的同时，还可以进行基于过程的程序设计，因而C++就适应的问题规模而论，大小由之。<br>
C++不仅拥有计算机高效运行的实用性特征，同时还致力于提高大规模程序的编程质量与程序设计语言的问题描述能力。

**适用设备：**

- MyCobotPro450

## 编程开发

### 推荐环境（与本工程一致）

**Ubuntu 20.04 LTS（64 位）**、**CMake ≥ 3.16**、**gcc/g++ 9.x**、**C++17**。详见 [环境搭建](./6.4.1-download.md)。

### 编译器

**GCC**、**Clang** 等支持 **C++17** 的工具链均可（以 [环境搭建](./6.4.1-download.md) 推荐版本为准）。

## C++ 开发使用引导（RobotDriver）

您可按以下顺序阅读 **6.4.x** 文档，使用 **RobotDriver** 对 **MyCobotPro450** 进行开发：

1. [环境搭建](./6.4.1-download.md)

2. [编译运行](./6.4.2-build.md)

3. [关节控制](./6.4.3-angle.md)

4. [坐标控制](./6.4.4-coord.md)

5. [IO 控制](./6.4.5-io.md)

6. [夹爪控制](./6.4.6-gripper.md)

7. [API 说明](./6.4.7-API.md)

8. [使用案例](./6.4.8-example.md)

---

[← 上一章](../6.2-ROS2/6.2.4-Moveit2/README.md) | [下一章 →](./6.4.1-download.md)
