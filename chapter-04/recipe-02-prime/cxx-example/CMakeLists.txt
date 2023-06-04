# set minimum cmake version
cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

# project name and language
project(recipe-02 LANGUAGES CXX)

# require C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# example library
add_library(sum_integers sum_integers.cpp)

# catch library
set(CATCH_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/catch)
add_library(Catch INTERFACE)
target_include_directories(Catch INTERFACE ${CATCH_INCLUDE_DIR})

# main code
add_executable(sum_up main.cpp)
target_link_libraries(sum_up sum_integers)

# testing binary
add_executable(cpp_test test.cpp)
target_link_libraries(cpp_test sum_integers Catch)

# enable testing functionality
enable_testing()

# define test
add_test(
  NAME catch_test
  COMMAND $<TARGET_FILE:cpp_test> --success
  )
