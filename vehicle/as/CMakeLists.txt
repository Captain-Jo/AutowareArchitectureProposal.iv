cmake_minimum_required(VERSION 3.0.2)
project(as)
add_compile_options(-std=c++14)

find_package(
  catkin REQUIRED COMPONENTS
  roscpp
  message_filters
  std_msgs
  geometry_msgs
  automotive_platform_msgs
  automotive_navigation_msgs
  pacmod_msgs
  can_msgs
  autoware_control_msgs
  autoware_vehicle_msgs
)

catkin_package(
  CATKIN_DEPENDS
  roscpp
  message_filters
  std_msgs
  geometry_msgs
  automotive_platform_msgs
  automotive_navigation_msgs
  pacmod_msgs
  can_msgs
  autoware_control_msgs
  autoware_vehicle_msgs
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_executable(pacmod_additional_debug_publisher
  src/pacmod_additional_debug_publisher/pacmod_additional_debug_publisher_node.cpp
  src/pacmod_additional_debug_publisher/pacmod_additional_debug_publisher_main.cpp
)
target_link_libraries(pacmod_additional_debug_publisher ${catkin_LIBRARIES})
add_dependencies(pacmod_additional_debug_publisher ${catkin_EXPORTED_TARGETS})

add_executable(ssc_interface
  src/ssc_interface/ssc_interface_node.cpp
  src/ssc_interface/ssc_interface.cpp
)
target_link_libraries(ssc_interface ${catkin_LIBRARIES})
add_dependencies(ssc_interface ${catkin_EXPORTED_TARGETS})

add_executable(pacmod_interface
  src/pacmod_interface/pacmod_interface.cpp
  src/pacmod_interface/pacmod_interface_node.cpp
)
target_link_libraries(pacmod_interface ${catkin_LIBRARIES})
add_dependencies(pacmod_interface ${catkin_EXPORTED_TARGETS})

install(TARGETS ssc_interface
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(TARGETS pacmod_interface
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(TARGETS pacmod_additional_debug_publisher
ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(
  DIRECTORY
    launch
    config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
