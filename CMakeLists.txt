cmake_minimum_required(VERSION 3.10)
project(LearnOpenGL)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Include directories
include_directories(
    external/glad/include
    external/glfw/include
    includes
)

# Add GLFW (must be before linking it)
add_subdirectory(external/glfw)

# Auto-add all .cpp files under src/*/* into executables
file(GLOB_RECURSE APP_SOURCES CONFIGURE_DEPENDS src/*/*.cpp)

foreach(source_file ${APP_SOURCES})
    get_filename_component(filename ${source_file} NAME_WE)  # e.g., hello_window

    add_executable(${filename} ${source_file} external/glad/src/glad.c)
    target_link_libraries(${filename} glfw dl m X11 pthread)
endforeach()

