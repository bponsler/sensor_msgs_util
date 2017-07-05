cmake_minimum_required(VERSION 3.5)
project(sensor_msgs_util)

# Add support for C++11
if(NOT WIN32)
  add_definitions(-std=c++11)
endif()

find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(rosidl_default_runtime REQUIRED)

ament_python_install_package(${PROJECT_NAME})

set(INCLUDE_DIRS include ${ament_cmake_INCLUDE_DIRS}
  ${geometry_msgs_INCLUDE_DIRS} ${builtin_interfaces_INCLUDE_DIRS}
  ${std_msgs_INCLUDE_DIRS} ${sensor_msgs_INCLUDE_DIRS} ${rosidl_default_generators_INCLUDE_DIRS}
  ${rosidl_default_runtime_INCLUDE_DIRS})
include_directories(${INCLUDE_DIRS})

set(LIBRARY_DIRS ${ament_cmake_LIBRARY_DIRS} ${geometry_msgs_LIBRARY_DIRS}
  ${builtin_interfaces_LIBRARY_DIRS} ${std_msgs_LIBRARY_DIRS} ${sensor_msgs_LIBRARY_DIRS} 
  ${rosidl_default_generators_LIBRARY_DIRS} ${rosidl_default_runtime_LIBRARY_DIRS})

link_directories(${LIBRARY_DIRS})

set(LIBS ${ament_cmake_LIBRARIES} ${geometry_msgs_LIBRARIES}
  ${builtin_interfaces_LIBRARIES} ${std_msgs_LIBRARIES} ${sensor_msgs_LIBRARIES} 
  ${rosidl_default_generators_LIBRARIES} ${rosidl_default_runtime_LIBRARIES})

# Install all headers
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION include/${PROJECT_NAME}
  FILES_MATCHING
  PATTERN "*.h")

if(BUILD_TESTING)
  add_subdirectory(test)
endif()

ament_export_dependencies(ament_cmake)
ament_export_dependencies(geometry_msgs)
ament_export_dependencies(builtin_interfaces)
ament_export_dependencies(std_msgs)
ament_export_dependencies(sensor_msgs)
ament_export_dependencies(rosidl_default_generators)
ament_export_dependencies(rosidl_default_runtime)
ament_export_include_directories(${INCLUDE_DIRS})

ament_package()
