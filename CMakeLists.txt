# Requirements
cmake_minimum_required(VERSION 3.0.0)

# Project settings
set(VERSION 1.0.0) 
set(DESCRIPTION "Ed25519 C implementation")
project(ed25519 VERSION ${VERSION} DESCRIPTION ${DESCRIPTION} LANGUAGES C)

# Build settings
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_OSX_SYSROOT /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk)
set(CMAKE_OSX_DEPLOYMENT_TARGET "10.11")
set(DEFAULT_BUILD_TYPE "Release")

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    message(STATUS "Setting build type to '${DEFAULT_BUILD_TYPE}'")
    set(CMAKE_BUILD_TYPE "${DEFAULT_BUILD_TYPE}" CACHE STRING "Choose the type of build." FORCE)
    
    # Set the possible values of build type for cmake-gui
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif()

if(NOT CMAKE_INSTALL_LIBDIR)
    set(CMAKE_INSTALL_LIBDIR lib/${PROJECT_NAME})
endif()

if(NOT CMAKE_INSTALL_INCLUDEDIR)
    set(CMAKE_INSTALL_INCLUDEDIR include/${PROJECT_NAME})
endif()

# Includes
include(GNUInstallDirs)

# Sources
file(GLOB_RECURSE SOURCES "src/*.c")

# Target
add_library(ed25519 STATIC ${SOURCES})
set_target_properties(ed25519 PROPERTIES VERSION ${VERSION})
set_target_properties(ed25519 PROPERTIES SOVERSION 1)

# Headers
include_directories(ed25519 PUBLIC include)

# Install
install(TARGETS ed25519
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
