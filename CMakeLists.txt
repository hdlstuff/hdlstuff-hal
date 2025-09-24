cmake_minimum_required(VERSION 3.15)
project(hdlstuff_hal)

set(CMAKE_CXX_STANDARD 20)

add_library(
    hdlstuff_hal
    STATIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src/hal.cpp
)

target_include_directories(
    hdlstuff_hal
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/hdlstuff_hal-config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/hdlstuff_hal-config.cmake @ONLY
)

install(
    TARGETS hdlstuff_hal
    EXPORT hdlstuff_hal-targets
    DESTINATION lib
)

install(
    DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/include"
    DESTINATION "${CMAKE_INSTALL_PREFIX}"
)

install(
    EXPORT hdlstuff_hal-targets
    NAMESPACE hdlstuff::
    DESTINATION "${CMAKE_INSTALL_PREFIX}/lib/hdlstuff_hal"
    COMPONENT dev
)

install(
    FILES ${CMAKE_CURRENT_BINARY_DIR}/hdlstuff_hal-config.cmake
    DESTINATION "${CMAKE_INSTALL_PREFIX}/lib/hdlstuff_hal"
)

export(PACKAGE hdlstuff_hal)
