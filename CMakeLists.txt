cmake_minimum_required(VERSION 3.0.0)

include(GNUInstallDirs)

project(ed25519 C)
set(DESCRIPTION "Ed25519 C implementation")

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
    src/sha512.c
)

include_directories(ed25519 PUBLIC include)

install(TARGETS ed25519
    EXPORT ${PROJECT_NAME}-targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

set(HEADERS include/ed25519.h include/fe.h include/fixedint.h include/ge.h include/precomp_data.h include/sc.h include/sha512.h)
install(FILES ${HEADERS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(EXPORT ${PROJECT_NAME}-targets DESTINATION cmake)
