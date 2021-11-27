cmake_minimum_required(VERSION 3.0.2)
project(selected_points_publisher)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rviz
)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)
find_package(PCL REQUIRED)

# catkin_python_setup()

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs  # Or other packages containing msgs
# )

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES bing_pannel
#  CATKIN_DEPENDS roscpp rviz
#  DEPENDS system_lib
)

###########
## Build ##
###########
include_directories(
# include
  ${catkin_INCLUDE_DIRS}
${PCL_INCLUDE_DIRS}
)
link_directories(${catkin_LIBRARY_DIRS})

set(CMAKE_AUTOMOC ON)

if(rviz_QT_VERSION VERSION_LESS "5")
  message(STATUS "Using Qt4 based on the rviz_QT_VERSION: ${rviz_QT_VERSION}")
  find_package(Qt4 ${rviz_QT_VERSION} EXACT REQUIRED QtCore QtGui)
  include(${QT_USE_FILE})
else()
  message(STATUS "Using Qt5 based on the rviz_QT_VERSION: ${rviz_QT_VERSION}")
  find_package(Qt5 ${rviz_QT_VERSION} EXACT REQUIRED Core Widgets)
  set(QT_LIBRARIES Qt5::Widgets)
endif()

add_definitions(-DQT_NO_KEYWORDS)
set(SOURCE_FILES
  src/SelectedPointsPublisher.cpp ##这里是你的主文件
  ${MOC_FILES}
)
add_library(selected_points_publisher ${SOURCE_FILES})

target_link_libraries(selected_points_publisher ${QT_LIBRARIES} ${catkin_LIBRARIES} ${PCL_LIBRARIES})


###########
##install##
###########

install(TARGETS
  selected_points_publisher
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(FILES
  plugin_discription.xml ##这里是你的plugin_discription.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
