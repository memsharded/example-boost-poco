cmake_minimum_required(VERSION 2.8)
project(BoostPoco)

if(EXISTS ${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
  include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
  conan_basic_setup()
endif()

find_package(Boost REQUIRED)

add_executable(timer timer.cpp)
target_link_libraries(timer ${CONAN_LIBS})
