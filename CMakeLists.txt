cmake_minimum_required(VERSION 3.15)
project(lumencpp LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS src/*.cpp)

add_library(lumencpp SHARED ${SOURCES})
add_library(lumencpp_static STATIC ${SOURCES})

target_include_directories(lumencpp PRIVATE include)
target_include_directories(lumencpp_static PRIVATE include)

set_target_properties(lumencpp_static PROPERTIES OUTPUT_NAME lumencpp)

install(TARGETS lumencpp lumencpp_static)
install(DIRECTORY include/ DESTINATION include)
