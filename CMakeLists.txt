cmake_minimum_required(VERSION 3.5)

project(libgnurx VERSION 2.5 LANGUAGES C)

set(CMAKE_C_STANDARD 90)

add_library(gnurx STATIC
    regcomp.c
    regex.c
    regex.h
    regexec.c
    regex_internal.c
    regex_internal.h
)

target_compile_definitions(gnurx PRIVATE -DHAVE_STDINT_H -DHAVE_LOCALE_H)
target_include_directories(gnurx PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
