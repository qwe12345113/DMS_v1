cmake_minimum_required (VERSION 3.1)
project (opencv-facial-landmark-detection LANGUAGES CXX)

# find all dependency libraries:
find_package(OpenMP)
if (NOT OPENMP_FOUND)
	message(WARNING "OpenMP is not found. Will be slow.")
else()
	set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()


find_package(OpenCV REQUIRED)
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/dlib-19.24/dlib/)

add_definitions(-O3 -Wall -Wextra)


# find sources
file(GLOB SOURCES src/lib/*.hpp src/lib/*.cc)

# add_library(openpano ${SOURCES})	# TODO shared?
# target_link_libraries(openpano lodepng ${OpenCV_LIBS})

# add_executable(ofld src/facialLandmarkDetection.cpp)
add_executable(ofld src/facialLandmarkDetection.cpp)
target_link_libraries(ofld ${OpenCV_LIBS} dlib::dlib)



