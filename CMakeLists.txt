cmake_minimum_required (VERSION 2.6)
set(LIB_NAME libsamplerate)
project(${LIB_NAME})

# Default to debug if CMAKE_BUILD_TYPE is not set.
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE debug)
endif()
set(PROJECT_BUILD_TYPE ${CMAKE_BUILD_TYPE})

string(TOLOWER ${PROJECT_BUILD_TYPE} PROJECT_BUILD_TYPE)
message("PROJECT_BUILD_TYPE: ${PROJECT_BUILD_TYPE}")

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

set(PROJECT_INCLUDE_DIR
	${PROJECT_SOURCE_DIR}/src
	)

if(WIN32)
	set(PROJECT_INCLUDE_DIR
		${PROJECT_SOURCE_DIR}/Win32
		)
else()
	execute_process(COMMAND "autogen.sh")
endif()

include_directories("${PROJECT_INCLUDE_DIR}")
include_directories("${PROJECT_SOURCE_DIR}")

add_subdirectory(src)
add_subdirectory(tests)
