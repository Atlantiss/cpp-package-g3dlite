cmake_minimum_required(VERSION 3.20)

set(CMAKE_DISABLE_SOURCE_CHANGES ON)
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project(g3dlite VERSION 9.0 LANGUAGES C CXX)

find_package(ZLIB REQUIRED)
find_package(Threads REQUIRED)

add_definitions(-D_WIN32_WINNT=0x0601)
add_definitions(-DWIN32_LEAN_AND_MEAN)
add_definitions(-DNOMINMAX)

add_subdirectory(src/g3dlite)
