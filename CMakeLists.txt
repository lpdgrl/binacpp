cmake_minimum_required(VERSION 3.10)
project(binacpp LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(LIBWEBSOCKETS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lib/libwebsockets-2.4.0)
set(JSONCPP_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lib/jsoncpp-1.8.3)

set(SOURCES
    src/binacpp.cpp
    src/binacpp_utils.cpp
    src/binacpp_logger.cpp
    src/binacpp_websocket.cpp
    ${JSONCPP_DIR}/src/jsoncpp.cpp
)

find_package(CURL REQUIRED)

add_library(binacpp STATIC ${SOURCES})

target_include_directories(binacpp PUBLIC
    src
    ${LIBWEBSOCKETS_DIR}/include
    ${JSONCPP_DIR}/include
)

target_link_libraries(binacpp PUBLIC CURL::libcurl)