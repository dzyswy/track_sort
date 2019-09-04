########################################################################
IF(${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR})
    MESSAGE(FATAL_ERROR "Prevented in-tree built. This is bad practice.")
ENDIF(${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR})


########################################################################
# Project setup
########################################################################
CMAKE_MINIMUM_REQUIRED(VERSION 3.9.0)
PROJECT(track_sort CXX)
ENABLE_TESTING()

set(CMAKE_CXX_STANDARD 11)


if (UNIX)
	ADD_DEFINITIONS(-fpermissive)

endif()

find_package(OpenCV REQUIRED)
if(NOT OpenCV_FOUND)
	message("fail to find OpenCV")
else()
	include_directories(${OpenCV_INCLUDE_DIRS})
	SET(LIBS ${LIBS} ${OpenCV_LIBS})
	message(STATUS "OpenCV library status:")
	message(STATUS "    version: ${OpenCV_VERSION}")
	message(STATUS "    include: ${OpenCV_INCLUDE_DIRS}")
	message(STATUS "    library: ${OpenCV_INSTALL_PATH}")
	message(STATUS "    libs: ${OpenCV_LIBS}")
endif()




INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/src)

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/src TRACK_SORT_SRCS)



add_executable(${PROJECT_NAME} ${TRACK_SORT_SRCS})
target_link_libraries(${PROJECT_NAME} ${LIBS})
