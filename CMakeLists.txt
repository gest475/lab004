cmake_minimum_required(VERSION 3.10)
project(lab04)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Библиотека print
add_library(print STATIC ${CMAKE_SOURCE_DIR}/sources/print.cpp)
target_include_directories(print PUBLIC ${CMAKE_SOURCE_DIR}/include)

# Пример 1
add_executable(example1 ${CMAKE_SOURCE_DIR}/examples/example1.cpp)
target_link_libraries(example1 print)

# Пример 2
add_executable(example2 ${CMAKE_SOURCE_DIR}/examples/example2.cpp)
target_link_libraries(example2 print)
