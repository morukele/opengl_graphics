cmake_minimum_required(VERSION 4.0)
project(graphics_programming)

set(CMAKE_CXX_STANDARD 20)

# --- Add GLFW using FetchContent ---
include(FetchContent)

FetchContent_Declare(
        glfw
        GIT_REPOSITORY https://github.com/glfw/glfw.git
        GIT_TAG latest
)

FetchContent_MakeAvailable(glfw)

# --- Add GLAD ---
add_library(glad src/glad.c)
target_include_directories(glad PUBLIC include)

add_executable(graphics_programming src/triangle.cpp)

target_link_libraries(graphics_programming PRIVATE glad glfw)
