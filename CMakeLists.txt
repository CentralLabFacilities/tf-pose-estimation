cmake_minimum_required(VERSION 2.8.3)
project(tfpose_ros)

## Add support for C++11, supported in ROS Kinetic and newer
add_definitions(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  roslaunch
  message_generation
)

# setup.py is called during catkin build
catkin_python_setup()

# Generate messages in the 'msg' folder
add_message_files(
  FILES
  BodyPartElm.msg
  Person.msg
  Persons.msg
)

generate_messages(
  DEPENDENCIES std_msgs
)

##################
## launch files ##
##################

roslaunch_add_file_check(launch)

catkin_package(
  CATKIN_DEPENDS rospy message_generation message_runtime
)
install(DIRECTORY launch
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install()

CATKIN_INSTALL_PYTHON(PROGRAMS scripts/broadcaster_ros.py DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
CATKIN_INSTALL_PYTHON(PROGRAMS scripts/visualization.py DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
