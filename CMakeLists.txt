# Set the name and the supported language of the project
project(hello-world-glade C)

# Set the minimum version of cmake required to build this project
cmake_minimum_required(VERSION 3.10)

# Use the package PkgConfig to detect GTK+ headers/library files
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK3 REQUIRED gtk+-3.0)

add_executable(hello-glade main.c)
target_link_libraries(hello-glade ${GTK3_LIBRARIES})

# Add other flags to the compiler
#target_compile_definitions(hello-glade PRIVATE ${GTK3_CFLAGS_OTHER})

# Add the -rdynamic flag
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -rdynamic")

# Setup CMake to use GTK+, tell the compiler where to look for headers
# and to the linker where to look for libraries
target_include_directories(hello-glade PRIVATE ${GTK3_INCLUDE_DIRS})
target_link_directories(hello-glade PRIVATE ${GTK3_LIBRARY_DIRS})
