cmake_minimum_required(VERSION 2.6)
project (${LIB_NAME}_test)
 
ADD_DEFINITIONS(-D_SCL_SECURE_NO_WARNINGS)

include_directories("${CMAKE_SOURCE_DIR}/src")

set(test_sources
	${CMAKE_CURRENT_SOURCE_DIR}/calc_snr.c
	${CMAKE_CURRENT_SOURCE_DIR}/util.c
)

# add all files in test directory..
file(GLOB PROJECT_TESTS_AUTO ${CMAKE_CURRENT_SOURCE_DIR}/*.c)
# .. and remove utility files
list(REMOVE_ITEM PROJECT_TESTS_AUTO ${CMAKE_CURRENT_SOURCE_DIR}/calc_snr.c)
list(REMOVE_ITEM PROJECT_TESTS_AUTO ${CMAKE_CURRENT_SOURCE_DIR}/src-evaluate.c)
list(REMOVE_ITEM PROJECT_TESTS_AUTO ${CMAKE_CURRENT_SOURCE_DIR}/util.c)


foreach( sourcefile ${PROJECT_TESTS_AUTO} )
	get_filename_component(testname ${sourcefile} NAME_WE)
	add_executable( ${testname} ${sourcefile} ${test_sources})
	add_dependencies(${testname} ${LIB_NAME})
	target_link_libraries(${testname} ${LIB_NAME}_static)
endforeach( sourcefile ${PROJECT_TESTS_AUTO} )
