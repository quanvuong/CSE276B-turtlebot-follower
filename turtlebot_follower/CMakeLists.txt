cmake_minimum_required(VERSION 2.8.3)
project(quan_turtlebot_follower_github)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS nodelet roscpp visualization_msgs turtlebot_msgs depth_image_proc dynamic_reconfigure)
find_package(Boost REQUIRED)

generate_dynamic_reconfigure_options(cfg/Follower.cfg)

catkin_package(
  INCLUDE_DIRS
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS nodelet roscpp visualization_msgs turtlebot_msgs depth_image_proc dynamic_reconfigure
)

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
)

## Declare a cpp library
add_library(${PROJECT_NAME} src/follower.cpp)

add_dependencies(${PROJECT_NAME}
  ${catkin_EXPORTED_TARGETS}
  ${PROJECT_NAME}_gencfg
  ${turtlebot_msgs_EXPORTED_TARGETS}
)

## Specify libraries to link a library or executable target against
target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
)

