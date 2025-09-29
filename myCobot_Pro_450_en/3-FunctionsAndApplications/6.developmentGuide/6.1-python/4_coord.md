## Coordinate control

It is mainly used to realize intelligent route planning to let the robot arm move from one position to another specified position. It is divided into `[x, y, z, rx, ry, rz]`, where `[x, y, z]` represents the position of the robot head in space (the coordinate system is the [rectangular coordinate system](https://zhidao.baidu.com/question/2125035227927850747.html)), and `[rx, ry, rz]` represents the posture of the robot head at this point (the coordinate system is the Euler coordinate system). The implementation of the algorithm and the representation of Euler coordinates require certain academic knowledge. We will not explain it too much here. As long as we understand the rectangular coordinate system, we can use this function well.

> **Note:** When setting coordinates, different series of robot arm joint structures are different. For the same set of coordinates, different series of robot arms will show different postures.
>
> <img src="../../../resources\3-FunctionsAndApplications\6.developmentGuide\python\axis/coordinate.jpg" style="zoom: 67%;" />

**Example Use**

```python
import time
from pymycobot import Pro450Client

pro450 = Pro450Client('192.168.0.232', 4500) # Client connection communication

print(pro450.get_coords()) # Read coordinate attitude information

pro450.send_angles([0, -10, -123, 45, 0, 0], 50) # Send angular motion to a certain attitude for coordinate control, speed is 50

time.sleep(3)

pro450.send_coord(1, 200, 50) # Send single coordinate control, speed is 50, so that the X axis moves to the position of 200mm

time.sleep(2)

pro450.send_coords([300, 86.8, 256.9, -178.0, 0.0, -90.0], 50) # Send multi-coordinate control, speed is 50
time.sleep(3)
```

---

[← Previous Chapter](./3_angle.md) | [Next Chapter→](./5_IO.md)