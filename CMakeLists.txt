cmake_minimum_required(VERSION 3.0.0)
project(ps1_opengl VERSION 0.0.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(DEPEND_DIR "${CMAKE_CURRENT_SOURCE_DIR}/dependencies")
set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")

# Add dependency subdir
add_subdirectory(dependencies)

## Find Dependencies
find_package(pxr REQUIRED)
find_package(glfw3 3.3 REQUIRED)
find_package(OpenGL REQUIRED)

include_directories(${PROJECT_NAME} ${DEPEND_DIR}/glad/include)

# Configure RPATH so libraries are found after make install
if(APPLE)
    set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
elseif(UNIX)
    set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib64")
endif()

add_executable(${PROJECT_NAME} ${SRC_DIR}/main.cpp)

# Add source subdir
add_subdirectory(src)

include_directories(${PROJECT_NAME} ${PXR_INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME}
        PRIVATE
        imgui
        glfw
        glad
        ${PXR_LIBRARIES}
)
