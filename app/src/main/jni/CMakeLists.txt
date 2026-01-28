cmake_minimum_required(VERSION 3.25.1)

project(MyLibName)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -w -s -Wno-error=format-security -fvisibility=hidden -fpermissive")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -w -s -Wno-error=format-security -fvisibility=hidden -Werror -std=c++17")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-error=c++11-narrowing -fpermissive -Wall -fexceptions")

set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -Wl,--gc-sections,--strip-all")

set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -marm")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -marm")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_library(
        MyLibName
        SHARED
        Main.cpp
        Substrate/hde64.c
        Substrate/SubstrateDebug.cpp
        Substrate/SubstrateHook.cpp
        Substrate/SubstratePosixMemory.cpp
        Substrate/SymbolFinder.cpp
        KittyMemory/KittyMemory.cpp
        KittyMemory/MemoryPatch.cpp
        KittyMemory/MemoryBackup.cpp
        KittyMemory/KittyUtils.cpp
        And64InlineHook/And64InlineHook.cpp
)

target_link_libraries(
        MyLibName
        log
        android
        EGL
        GLESv2
)