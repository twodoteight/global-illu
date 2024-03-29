cmake_minimum_required(VERSION 3.2)

project(global-illu)

set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 14)

set(SOURCES main.cpp)
set(HEADERS include/gui.h include/image.h include/ray.h include/entities.h include/camera.h include/raytracer.h include/viewer.h include/octree.h include/bbox.h include/material.h)

find_package(Qt5Widgets)
find_package(Threads)

if (MSVC)
add_definitions(-DNOMINMAX)
endif()

add_executable(global-illu ${SOURCES} ${HEADERS})
include_directories(global-illu include 3rd_party)

option(CLANG_FORMAT_TARGET "automatic clang format" OFF)
if(CLANG_FORMAT_TARGET)
    include(ClangFormat)
    add_clang_format(TARGET global-illu STYLE "LLVM" FILES ${SOURCES} ${HEADERS})
endif(CLANG_FORMAT_TARGET)


target_link_libraries(global-illu Qt5::Widgets ${CMAKE_THREAD_LIBS_INIT})

