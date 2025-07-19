cmake_minimum_required(VERSION 3.2...3.10)

project(libgnurx VERSION 2.5 LANGUAGES C)

include(GNUInstallDirs)

set(CMAKE_C_STANDARD 90)

add_library(gnurx STATIC
    regcomp.c
    regex.c
    regex.h
    regexec.c
    regex_internal.c
    regex_internal.h
)

if("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Werror-implicit-function-declaration")
endif()

target_compile_definitions(gnurx PRIVATE -DHAVE_STDINT_H -DHAVE_LOCALE_H)
target_include_directories(gnurx PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")

install(FILES regex.h DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")

install(TARGETS gnurx
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)
