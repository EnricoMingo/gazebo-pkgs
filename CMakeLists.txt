cmake_minimum_required(VERSION 2.8.12)
if(COMMAND cmake_policy)
    cmake_policy(SET CMP0003 OLD)
    cmake_policy(SET CMP0005 NEW)
    cmake_policy(SET CMP0017 NEW)
endif(COMMAND cmake_policy)
include(ExternalProject)

#if(${UBUNTU_VERSION} MATCHES "xenial")
     message(STATUS "Adding CXX support")
    include(CheckCXXCompilerFlag)
    check_cxx_compiler_flag("-std=c++11" COMPILER_SUPPORTS_CXX11)
    check_cxx_compiler_flag("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
    if(COMPILER_SUPPORTS_CXX11)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
    elseif(COMPILER_SUPPORTS_CXX0X)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
    else()
        message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
    endif()
#endif(${UBUNTU_VERSION} MATCHES "xenial")

set(CMAKE_ROOT_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(CMAKE_CURRENT_SOURCE_DIR ${CMAKE_ROOT_SOURCE_DIR}/gazebo_grasp_plugin) 

include(${CMAKE_CURRENT_SOURCE_DIR}/CMakeLists.txt)
#include(${CMAKE_CURRENT_SOURCE_DIR}/gazebo_state_plugins/CMakeLists.txt)
#include(${CMAKE_CURRENT_SOURCE_DIR}/gazebo_test_tools/CMakeLists.txt)
#include(${CMAKE_CURRENT_SOURCE_DIR}/gazebo_world_plugin_loader/CMakeLists.txt)
