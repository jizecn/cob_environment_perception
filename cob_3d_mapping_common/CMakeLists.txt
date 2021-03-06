cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

# add dynamic reconfigure api
rosbuild_find_ros_package(dynamic_reconfigure)
include(${dynamic_reconfigure_PACKAGE_PATH}/cmake/cfgbuild.cmake)
gencfg()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/ros/include
    ${PROJECT_SOURCE_DIR}/common/include  )

#rosbuild_add_library(gpc common/src/gpc.c)

rosbuild_add_library(cob_3d_mapping_common
	common/src/shape.cpp
	common/src/shape_cluster.cpp
	common/src/polygon.cpp
	common/src/cylinder.cpp
	common/src/gpc.c)
#target_link_libraries(cob_3d_mapping_common )


rosbuild_add_executable(field_of_view_node ros/src/field_of_view.cpp)
rosbuild_add_executable(keyframe_detector_node ros/src/keyframe_detector.cpp)
rosbuild_add_executable(transform_shape_array ros/src/transform_shape_array.cpp)
target_link_libraries(transform_shape_array cob_3d_mapping_common )
#rosbuild_add_library(cob_3d_mapping_common_sv ros/src/shape_visualization.cpp)

#~~~~~~~~~
#rosbuild_add_executable(cylinder common/src/cyl_test.cpp)
#target_link_libraries(cylinder cob_3d_mapping_common )
#~~~~~~~~~

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})
rosbuild_add_roslaunch_check(ros/launch)
