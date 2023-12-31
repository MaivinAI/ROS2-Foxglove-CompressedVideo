cmake_minimum_required(VERSION 3.5)
project(foxglove_msgs)

if(NOT CMAKE_CXX_STANDARD)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)

file(GLOB _all_msg_files RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" msg/*)
message(STATUS "Using msg files: ${_all_msg_files}")
if(NOT _all_msg_files)
message(FATAL_ERROR "No msg files found")
endif()

rosidl_generate_interfaces(${PROJECT_NAME}
${_all_msg_files}
DEPENDENCIES builtin_interfaces
ADD_LINTER_TESTS
)

ament_export_dependencies(rosidl_default_runtime)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
