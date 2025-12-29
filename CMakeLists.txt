cmake_minimum_required(VERSION 3.16)

project(LA16ASM LANGUAGES C)

include(FetchContent)

FetchContent_Declare(
    la16
    GIT_REPOSITORY https://github.com/lightweight-architecture/la16.git
    GIT_TAG main
)

FetchContent_Declare(
    lautils
    GIT_REPOSITORY https://github.com/lightweight-architecture/lautils.git
    GIT_TAG main
)

FetchContent_MakeAvailable(la16)
FetchContent_MakeAvailable(lautils)

add_executable(la16asm
    src/main.c
    src/cmptok.c
    src/code.c
    src/compile.c
    src/compiler.c
    src/constant.c
    src/label.c
    src/opcode.c
    src/parse.c
    src/register.c
    src/section.c
)

target_include_directories(la16asm
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(la16asm
    PRIVATE la16_headers
    PRIVATE lautils
)

target_compile_features(la16asm PRIVATE c_std_99)