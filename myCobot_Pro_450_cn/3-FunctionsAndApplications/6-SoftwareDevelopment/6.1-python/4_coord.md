# 坐标控制

主要用于实现智能规划路线让机械臂从一个位置到另一个指定位置。分为`[x,y,z,rx,ry,rz]`，其中`[x,y,z]`表示的是机械臂头部在空间中的位置（该坐标系为[直角坐标系](https://zhidao.baidu.com/question/2125035227927850747.html)），`[rx,ry,rz]`表示的是机械臂头部在该点的姿态（该坐标系为欧拉坐标）。算法的实现以及欧拉坐标的表示需要一定的学术知识，这里不对其过多的讲解，我们只要懂得直角坐标系就可以很好的使用这个函数了。

> **注意：** 在设置坐标时，不同系列的机械臂关节构造有所不同，同一组坐标，不同系列的机械臂会展示不同的姿态。
>
> <img src="../../../resources\3-FunctionsAndApplications\6.developmentGuide\python\axis/坐标.jpg" style="zoom: 67%;" />

**案例使用**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500)  # 客户端连接通信

print(pro450.get_coords())  # 读取坐标姿态信息

pro450.send_angles([0, -10, -123, 45, 0, 0], 50)  # 发送角运动到某一姿态以进行坐标控制，速度为 50
time.sleep(3)

pro450.send_coord(1, 200, 50)  # 发送单坐标控制，速度为50，使X轴运动到200mm的位置
time.sleep(2)

pro450.send_coords([300, 86.8, 256.9, -178.0, 0.0, -90.0], 50) # 发送多坐标控制，速度为50
time.sleep(3)
```

---

[← 上一章](./3_angle.md) | [下一章 →](./5_IO.md)