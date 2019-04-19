# Requirements
cmake_minimum_required(VERSION 3.0.0)
include(GNUInstallDirs)

# Project settings
set(VERSION 1.0.0) 
set(DESCRIPTION "Ed25519 C implementation")
project(ed25519)

# Build settings
set(CMAKE_CXX_STANDARD 11)
set(DEFAULT_BUILD_TYPE "Release")

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    message(STATUS "Setting build type to '${DEFAULT_BUILD_TYPE}'")
    set(CMAKE_BUILD_TYPE "${DEFAULT_BUILD_TYPE}" CACHE STRING "Choose the type of build." FORCE)
    
    # Set the possible values of build type for cmake-gui
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif()


# Target
add_library(ed25519 STATIC 
    src/add_scalar.c
    src/fe.c
    src/ge.c
    src/key_exchange.c
    src/keypair.c
    src/sc.c
    src/seed.c
    src/sign.c
    src/verify.c
    src/sha256.c
)

set(HEADERS include/ed25519.h include/fe.h include/fixedint.h include/ge.h include/precomp_data.h include/sc.h include/sha512.h)
set_target_properties(ed25519 PROPERTIES VERSION ${VERSION})
set_target_properties(ed25519 PROPERTIES SOVERSION 1)

# Headers
include_directories(ed25519 PUBLIC include)

# Install
install(TARGETS ed25519
    EXPORT ${PROJECT_NAME}-targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION  ${CMAKE_INSTALL_LIBDIR}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
    
install(FILES ${HEADERS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
