cmake_minimum_required(VERSION 2.6)
project (${LIB_NAME})
 
ADD_DEFINITIONS(-D_SCL_SECURE_NO_WARNINGS)

file(GLOB PROJECT_SRCS_AUTO ${CMAKE_CURRENT_SOURCE_DIR}/*.c)

add_library(${PROJECT_NAME} SHARED ${PROJECT_SRCS_AUTO})
add_library(${PROJECT_NAME}_static STATIC ${PROJECT_SRCS_AUTO})

### OS specific stuff ###
if(NOT WIN32)
	install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION lib)
	install(DIRECTORY ../include/ DESTINATION include/${PROJECT_NAME})
endif()
#########################
