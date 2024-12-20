cmake_minimum_required(VERSION 3.0.0)
project(hello_window VERSION 1.0.0)

## Find Dependencies
find_package(glfw3 3.3 REQUIRED)
find_package(imgui REQUIRED)



add_executable(hello_window 
        src/config.h 
        src/main.cpp
        src/glad.c)

target_include_directories(hello_window PRIVATE dependencies)

target_link_libraries(hello_window glfw)
