cmake_minimum_required(VERSION 2.8.3)
project(odom_array_msgs)

find_package(catkin REQUIRED COMPONENTS
  message_generation
  std_msgs
  nav_msgs
)

add_message_files(
  FILES
  OdometryArray.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
  nav_msgs
)

catkin_package(
  CATKIN_DEPENDS message_runtime std_msgs nav_msgs
)
