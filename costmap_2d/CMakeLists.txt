cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
set(ROS_BUILD_TYPE Release)
rosbuild_init()
rosbuild_genmsg()

#rosbuild_add_boost_directories()

rosbuild_add_library(costmap_2d src/costmap_2d.cpp src/observation_buffer.cpp src/costmap_2d_ros.cpp src/costmap_2d_publisher.cpp src/voxel_costmap_2d.cpp)
#rosbuild_link_boost(costmap_2d thread)

rosbuild_find_ros_package(dynamic_reconfigure)
include(${dynamic_reconfigure_PACKAGE_PATH}/cmake/cfgbuild.cmake)
gencfg()


rosbuild_add_executable(bin/costmap_2d_markers src/costmap_2d_markers.cpp)
rosbuild_add_executable(bin/costmap_2d_cloud src/costmap_2d_cloud.cpp)

rosbuild_add_executable(bin/costmap_2d_node src/costmap_2d_node.cpp)
target_link_libraries(bin/costmap_2d_node costmap_2d)
