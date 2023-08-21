cmake_minimum_required(VERSION 2.8.3)
project(demo_lidar)

SET(CMAKE_BUILD_TYPE Release)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall  -O3 -march=native ")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall   -O3 -march=native")


set(BUILD_STATIC_LIBS ON)
set(BUILD_SHARED_LIBS OFF)
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

# Find catkin macros and libraries
find_package(catkin REQUIRED
             COMPONENTS roscpp
                        std_msgs
                        sensor_msgs
                        cv_bridge
                        pcl_ros)
#set(OpenCV_DIR "/home/leone/ros-kinetic/src/opencv3/install/share/OpenCV-3.3.1-dev")
#set(OpenCV_DIR "/home/leone/Documents/software/opencv-2.4.13.6/install/share/OpenCV")
find_package(OpenCV 3 REQUIRED)

#set(PCL_DIR "/home/leone/Documents/software/pcl-pcl-1.7.2/install/share/pcl-1.7")

find_package(PCL 1.7 REQUIRED)
find_package(Eigen3 REQUIRED)

#
# catkin specific configuration ##
#

catkin_package(CATKIN_DEPENDS roscpp std_msgs sensor_msgs cv_bridge pcl_ros)

#
# Build ##
#

# Specify additional locations of header files Your package locations should be
# listed before other locations
include_directories(${catkin_INCLUDE_DIRS}
  #${OpenCV_INCLUDE_DIRS}
                    ${PCL_INCLUDE_DIRS}
                    ${EIGEN3_INCLUDE_DIR}
                    "${PROJECT_SOURCE_DIR}/include"
                    #/usr/local/include # Location when using 'make
                    #/home/leone/ros-kinetic/src/opencv3/install/include/opencv-3.3.1-dev                   # system_install'
                    #/home/leone/Documents/software/opencv-2.4.13.6/install
                    #/home/leone/Documents/software/opencv-2.4.13.6/install/include/
                    #/home/leone/Documents/software/opencv-3.3.1/install/include/
                    ${OpenCV_INCLUDE_DIRS}
                    # system_install'
                    #/usr/include # More usual location (e.g. when installing
                                 # using a package)
                    )

# Specify additional locations for library files
link_directories(/usr/local/lib # Location when using 'make system_install'
                 /usr/lib # More usual location (e.g. when installing using a
                          # package)
                 )

add_subdirectory(isamlib)
link_libraries(isamlib)

# Declare executables
add_executable(featureTracking src/featureTracking.cpp)
add_executable(visualOdometry src/visualOdometry.cpp)
add_executable(bundleAdjust src/bundleAdjust.cpp)
add_executable(processDepthmap src/processDepthmap.cpp)
add_executable(stackDepthPoint src/stackDepthPoint.cpp)
add_executable(transformMaintenance src/transformMaintenance.cpp)
add_executable(registerPointCloud src/registerPointCloud.cpp)

# Specify libraries to link a library or executable target against
target_link_libraries(featureTracking
                      ${catkin_LIBRARIES}
                      ${OpenCV_LIBRARIES}
                      ${PCL_LIBRARIES})
target_link_libraries(visualOdometry
                      ${catkin_LIBRARIES}
                      ${OpenCV_LIBRARIES}
                      ${PCL_LIBRARIES})
target_link_libraries(bundleAdjust
                      ${catkin_LIBRARIES}
                      ${OpenCV_LIBRARIES}
                      ${PCL_LIBRARIES})
target_link_libraries(processDepthmap
                      ${catkin_LIBRARIES}
                      ${OpenCV_LIBRARIES}
                      ${PCL_LIBRARIES})
target_link_libraries(stackDepthPoint
                      ${catkin_LIBRARIES}
                      ${OpenCV_LIBRARIES}
                      ${PCL_LIBRARIES})
target_link_libraries(transformMaintenance
                      ${catkin_LIBRARIES}
                      ${OpenCV_LIBRARIES}
                      ${PCL_LIBRARIES})
target_link_libraries(registerPointCloud
                      ${catkin_LIBRARIES}
                      ${OpenCV_LIBRARIES}
                      ${PCL_LIBRARIES})
