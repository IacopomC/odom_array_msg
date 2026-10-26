# odom_array_msgs

A small, standalone ROS 2 (ament) message package. It provides a single
message type, `OdometryArray`, for carrying several `nav_msgs/Odometry`
estimates together in one timestamped message.

## Message

`OdometryArray.msg`:

```
std_msgs/Header     header
nav_msgs/Odometry[] odometries
```

The `header` gives a common timestamp and frame for the whole batch.
`odometries` is a variable length array in which every element is a standard
`nav_msgs/Odometry` (pose and twist, each with covariance). This is handy when
a node needs to publish many odometry estimates captured at the same instant,
for example several moving objects observed in a single frame, without creating
a separate topic for each one.

## Dependencies

`std_msgs`, `nav_msgs`, and the ROS 2 interface tooling (`rosidl_default_generators`
at build time, `rosidl_default_runtime` at run time).

## Build

Place the package inside a colcon workspace `src` folder and build it:

```
colcon build --packages-select odom_array_msgs
```

Once the workspace is sourced, the message is available as
`odom_array_msgs/msg/OdometryArray` from both C++ and Python.

## Usage

C++:

```cpp
#include <odom_array_msgs/msg/odometry_array.hpp>

odom_array_msgs::msg::OdometryArray msg;
msg.header.stamp = node->now();
msg.header.frame_id = "map";

nav_msgs::msg::Odometry odom;
// populate odom.pose and odom.twist
msg.odometries.push_back(odom);
```

Python:

```python
from odom_array_msgs.msg import OdometryArray
from nav_msgs.msg import Odometry

msg = OdometryArray()
msg.header.stamp = node.get_clock().now().to_msg()
msg.header.frame_id = "map"
msg.odometries.append(Odometry())
```

## License

MIT.
