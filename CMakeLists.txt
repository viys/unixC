cmake_minimum_required(VERSION 3.15)

#c99
set(CMAKE_C_FLAGS "-std=c99")

project(hello)

# 将可执行文件输出到指定路径
# set(HOME ..)
# set(EXECUTABLE_OUTPUT_PATH ${HOME}/bin)

# add the executable
file(GLOB_RECURSE SRC ${CMAKE_CURRENT_SOURCE_DIR}/app/*.c)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/bsp)

# file(GLOB_RECURSE SRC ${CMAKE_CURRENT_SOURCE_DIR}/third-party/*.c)
add_definitions(-DSHELL_CFG_USER="shell_cfg_user.h")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} \
    -T \"${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/shell.lds\" \
    -Wl,-Map=LetterShell.map")
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/src)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/extensions)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/extensions/cpp_support)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/extensions/fs_support)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/extensions/game)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/extensions/log)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/extensions/shell_enhance)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/app/third-party/letter_shell/extensions/telnet)

add_executable(hello ${SRC})