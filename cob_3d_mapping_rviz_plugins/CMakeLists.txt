cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
set(ROS_BUILD_TYPE RelWithDebInfo)


rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
rosbuild_genmsg()

#uncomment if you have defined services
rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#target_link_libraries(example ${PROJECT_NAME})


#set( BUT_COB_TELEOP_PROJECT_NAME but_cob_teleop )
#rosbuild_add_library( ${BUT_COB_TELEOP_PROJECT_NAME} ${BUT_COB_TELEOP_SOURCE_FILES} )

#rosbuild_add_executable(but_cob_teleop_marker src/but_cob_teleop/but_cob_teleop.cpp)
#target_link_libraries(but_cob_teleop_marker ${BUT_COB_TELEOP_PROJECT_NAME})

# BUT services
#set( BUT_SERVICES_SOURCE_FILES src/but_services/PointCloudTools.cpp
#                               src/but_services/but_service_server.cpp )

#set( BUT_SERVICES_PROJECT_NAME but_services )
rosbuild_add_library(cob_3d_mapping_rviz_plugins src/shape_display.cpp
    src/shape_base.cpp
    src/shape_marker.cpp
    src/polypartition.cpp
    src/init.cpp)
rosbuild_add_executable(cob_3d_mapping_rviz_plugins_test src/test.cpp)

#rosbuild_add_executable(map_publisher src/map_publisher.cpp)

#rosbuild_add_executable(but_service_server src/but_services/but_service_server.cpp)
#target_link_libraries(but_service_server ${BUT_SERVICES_PROJECT_NAME})



# BUT rviz display
#set( DISPLAY_SOURCE_FILES src/but_display/but_display.cpp
#                          src/but_display/but_pointcloud.cpp
#                          src/but_display/point_cloud_base.cpp
#                          src/but_display/but_arm_manipulation.cpp
#                          src/but_display/but_examplepane.cpp
#                          src/but_display/but_distance_visualizer.cpp
#			  			  src/but_data_fusion/but_cam_display.cpp
#			  			  src/but_display/but_camcast.cpp
#			  			  src/but_display/CRosRttTexture.cpp
#                          src/but_display/init.cpp )

#set( BUT_DISPLAY_PROJECT_NAME but_gui )
#include_directories(include/but_display include/but_data_fusion srv_gen/cpp/include/srs_ui_but/)
#rosbuild_add_library( ${BUT_DISPLAY_PROJECT_NAME} ${DISPLAY_SOURCE_FILES} )

# Add wx widgets
find_package(wxWidgets REQUIRED)
include(${wxWidgets_USE_FILE})
include_directories( ${wxWidgets_INCLUDE_DIRS} )

#target_link_libraries(${BUT_DISPLAY_PROJECT_NAME} ${wxWidgets_LIBRARIES} ${OGRE_LIBRARIES} )

# BUT data fusion
#rosbuild_add_executable(view src/but_data_fusion/view.cpp)
