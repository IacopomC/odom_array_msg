# odom_array_msgs

A small, standalone ROS 1 (catkin) message package. It provides a single
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

`std_msgs`, `nav_msgs`, and the catkin message tooling (`message_generation` at
build time, `message_runtime` at run time).

## Build

Place the package inside a catkin workspace `src` folder and build it:

```
catkin build odom_array_msgs
```

Once the workspace is sourced, the message is available as
`odom_array_msgs/OdometryArray` from both C++ and Python.

## Usage

C++:

```cpp
#include <odom_array_msgs/OdometryArray.h>

odom_array_msgs::OdometryArray msg;
msg.header.stamp = ros::Time::now();
msg.header.frame_id = "map";

nav_msgs::Odometry odom;
// populate odom.pose and odom.twist
msg.odometries.push_back(odom);
```

Python:

```python
import rospy
from odom_array_msgs.msg import OdometryArray
from nav_msgs.msg import Odometry

msg = OdometryArray()
msg.header.stamp = rospy.Time.now()
msg.header.frame_id = "map"
msg.odometries.append(Odometry())
```

## License

MIT.
