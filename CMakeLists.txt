cmake_minimum_required(VERSION 4.0)
project(graphics_programming)

set(CMAKE_CXX_STANDARD 20)

# --- Add global include directory ---
include_directories(include)

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

# --- Set common libraries here ---
set(COMMON_LIBS glad glfw)

# --- Add Executable for each file---
file(GLOB SOURCES "src/*.cpp")
foreach (SOURCE_FILE ${SOURCES})
    # --- Extract file name without extension ---
    get_filename_component(EXEC_NAME ${SOURCE_FILE} NAME_WE)

    # --- Create on executable per file ---
    add_executable(${EXEC_NAME} ${SOURCE_FILE})

    # --- Link OpenGL libraries
    target_link_libraries(${EXEC_NAME} PRIVATE ${COMMON_LIBS})
endforeach ()