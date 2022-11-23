# Minimum version of CMake required to build this project
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

# Name of the project
project(app)

find_package(OpenCV REQUIRED)

include_directories("${OpenCV_INCLUDE_DIRS}")

# Add all the source files needed to build the executable
add_executable(app main.cpp)

# Link the executable and the library together
target_link_libraries(app "${OpenCV_LIBS}")
set_property(TARGET app PROPERTY CXX_STANDARD 14)
