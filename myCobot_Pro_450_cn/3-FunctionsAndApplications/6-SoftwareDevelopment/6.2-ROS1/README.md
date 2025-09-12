# ROS

ROS 是开源的，是用于机器人控制的一种后操作系统，或者说次级操作系统。它提供类似操作系统所提供的功能，包含硬件抽象描述、底层驱动程序管理、共用功能的执行、程序间的消息传递、程序发行包管理，它也提供一些工具程序和库用于获取、建 立、编写和运行多机整合的程序。

ROS 运行时的 "图 "是一个基于 ROS 通信基础设施的松散耦合点对点进程网络。ROS 实现了多种不同的通信方法，包括基于同步 RPC 式通信的服务机制、基于异步流媒体数据的主题机制和用于数据存储的参数服务器。

ROS 并非实时框架，但可以嵌入实时程序中。Willow Garage 的 PR2 机器人使用一个名为 pr2_etherCAT 的系统来实时发送或接收 ROS 消息。ROS 还可以与 Orocos 实时工具包无缝集成。

**ROS Logo** ：

![ROS图标](../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROSicon.png)

## 1 ROS 的设计目标和特点

很多人问："ROS 和其他机器人软件平台有什么不同？这个问题很难回答。因为 ROS 并不是一个集成了大多数功能或特性的框架。事实上，ROS 的主要目标是为机器人研发提供代码重用支持。ROS 是一个用于分布式进程的框架（即节点），这些进程封装在程序和功能包中，可以轻松共享和分发。ROS 还支持类似于代码库的联合系统，该系统还能实现项目的协作和分发。这种设计使项目的开发和实现从文件系统到用户界面都可以完全独立决定（ROS 没有限制）。同时，所有项目都可以与 ROS 的基本工具集成。

为了支持共享和协作的主要目标，ROS 框架还具有其他一些功能：

- 精简：ROS 的设计尽可能精简，这样为 ROS 编写的代码就可以与其他机器人软件框架一起使用。由此必然得出的结论是，ROS 可以轻松集成到其他机器人软件平台中：ROS 已经可以与 OpenRAVE、Orocos 和 Player 集成。
- 对 ROS 不敏感的库：ROS 的首选开发模式是编写不依赖于 ROS 的简洁库函数。
- 语言独立性：ROS 框架可以简单地用任何现代编程语言实现。ROS 已经实现了 Python 版本、C++ 版本和 Lisp 版本。它还有 Java 和 Lua 版本的实验库。
- 松耦合：ROS 中的功能模块封装在独立的功能包或元功能包中，易于共享。功能包中的模块以节点为单位运行。使用 ROS 标准 IO 作为接口，开发人员无需关注模块的内部实现，只要了解接口规则，就能实现模块间的重用和点对点松耦合。
- 便捷的测试：ROS 内置名为 rostest 的单元/集成测试框架，可轻松安装或卸载测试模块。
- 可扩展：ROS 适用于大型运行系统和大型开发流程。
- 免费、开源：它有许多开发人员和许多功能包。

## 2 为什么使用 ROS？

通过 ROS，我们可以在虚拟环境中实现对机械臂的模拟控制。

我们将通过**rviz**将机械臂可视化，以多种方式操作机械臂，并通过**MoveIt**规划和执行机械臂的动作路径，从而达到自由控制机械臂的效果。

在接下来的章节中，我们将学习如何通过 ros 平台控制我们的产品。

# MoveIt

**MoveIt** 是目前最先进的机械臂运动操作软件，已用于 100 多台机器人。它集成了运动规划、控制、三维感知、运动控制、控制和导航等方面的最新成果，为开发先进的机器人应用提供了一个易于使用的平台，并为工业、商业、研发等领域的机器人新产品设计和集成评估提供了一个集成软件平台。

**MoveIt Logo** :

![moveit图标](../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/moveiticon.png)

## 1 说明

MoveIt 是一个 ROS 集成开发平台，由各种用于操纵机械臂的功能包组成，包括运动规划、操作、控制、逆运动学、三维感知、碰撞检测等。

下图显示了 Moveit 提供的主节点**move_group**的高层结构。它就像一个组合器：将所有单独的组件整合在一起，为用户提供一系列操作和服务。

<img src =../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS1/moveit/moveit-1.png
width ="500"  align = "center">

## 2 用户界面

用户可以通过三种方式访问 move_group 提供的操作和服务：

- 在 C++ 中，通过使用 move_group_interface 软件包，可以轻松使用 move_group。
- 在 Python 中，使用 moveit_commander 软件包。
- 通过图形用户界面：使用 Motion-commander 的 Rviz（ROS 可视化工具）。

move_group 可以通过 ROS 参数服务器进行配置，也可以通过该服务器获取机器人的 URDF 和 SRDF。

## 3 配置

move_group 是一个 ROS 节点。它使用 ROS 参数服务器获取三种信息：

- URDF - move_group 会在 ROS 参数服务器中查找 robot_description 参数，以获取机器人的 URDF。
- SRDF - move_group 会在 ROS 参数服务器中查找 robot_description_semantic 参数，以获取机器人的 SRDF。SRDF 通常由用户使用 MoveIt 设置助手创建。
- MoveIt configuration - move_group 将在 ROS 参数服务器中查找其他 MoveIt 特定配置，包括关节约束、运动学、运动规划、感知等信息。 这些组件的配置文件由 MoveIt 设置助手自动生成，并存储在机器人相应 MoveIt 配置包的配置目录中。有关配置助手的使用，请参阅： [MoveIt 安装助手](https://moveit.picknik.ai/main/doc/examples/setup_assistant/setup_assistant_tutorial.html)

---

[← 上一节](../6.1-python/README.md) | [下一页 →](./6.2.1-环境搭建.md)
