cmake_minimum_required(VERSION 3.10)
project(Project VERSION 0.1.0 LANGUAGES C)

set(Project_Name "Project")
set(SOURCE_DIR
	src/main.c
)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

if(GCC_PATH)
	set(CMAKE_C_COMPILER ${GCC_PATH})
else()
	set(CMAKE_C_COMPILER gcc)
endif()

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(NOT CMAKE_BUILD_TYPE)
	set(CMAKE_BUILD_TYPE Debug)
endif()

add_executable(${Project_Name} ${SOURCE_DIR})

target_include_directories(${Project_Name} PRIVATE /include)

target_compile_options(${Project_Name} PRIVATE
	-Wall -Wextra -Wpedantic -Wshadow -Wvla
	$<$<CONFIG:Debug>:-g -O0 -DDEBUG>
	$<$<CONFIG:Release>:-O2 -DNDEBUG>
)

set_target_properties(${Project_Name} PROPERTIES
	RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/bin/$<CONFIG>"
)
