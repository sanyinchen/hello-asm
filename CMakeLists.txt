cmake_minimum_required(VERSION 3.16)
set(project_name "nasm-hello_asm")
project(${project_name})


if (APPLE)
    set(CMAKE_ASM_NASM_OBJECT_FORMAT macho64)
    set(CMAKE_ASM_NASM_FLAGS "-DMACOS")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -macosx_version_min 10.13 -no_pie")
endif (APPLE)

if (UNIX AND NOT APPLE)
    set(CMAKE_ASM_NASM_OBJECT_FORMAT elf64)
endif (UNIX AND NOT APPLE)

enable_language(ASM_NASM)

set(CMAKE_NASM_LINK_EXECUTABLE "ld <LINK_FLAGS> <OBJECTS> -o <TARGET> <LINK_LIBRARIES>")
set(CMAKE_ASM_NASM_SOURCE_FILE_EXTENSIONS ${CMAKE_ASM_NASM_SOURCE_FILE_EXTENSIONS} s S)

set(SOURCE_FILES
        src/asm/hello.asm)

add_executable(${project_name} ${SOURCE_FILES})

set_target_properties(${project_name} PROPERTIES LINKER_LANGUAGE NASM)

if (APPLE)
    target_link_libraries(${project_name} System)
endif (APPLE)