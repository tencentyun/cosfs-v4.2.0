cmake_minimum_required(VERSION 2.8)
CMAKE_policy(SET CMP0015 NEW)

project(cosfs-v4.2.0)
SET(CMAKE_C_COMPILER g++)

option(CMAKE_BUILD_TYPE "Release")
if (CMAKE_BUILD_TYPE STREQUAL "Debug")
	message("debug mode")
	set(CMAKE_CXX_FLAGS "$ENV{CMAKE_CXX_FLAGS} -O0 -Wall -g")
	set(CMAKE_CXX_FLAGS_DEUBG "$ENV{CMAKE_CXX_FLAGS_DEUBG} -O0 -Wall -g")
else ()
	message("release mode")
endif()

include_directories(./include)
include_directories(./include/cos-cpp-sdk)
link_directories(./lib)
file(GLOB_RECURSE cosfs_source_files "./src/*.cpp")
ADD_EXECUTABLE(cosfs ${cosfs_source_files})
add_definitions(-D_FILE_OFFSET_BITS=64)
target_link_libraries(cosfs fuse dl cossdk curl ssl crypto rt jsoncpp
stdc++ pthread z boost_system boost_thread tcmalloc)
#set_target_properties(cosfs PROPERTIES OUTPUT_NAME "cosfs")
