CMAKE_MINIMUM_REQUIRED(VERSION 3.14) # pi

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

PROJECT(sharedlua LANGUAGES C)

ADD_LIBRARY(sharedlua SHARED
    lapi.c
    lauxlib.c
    lbaselib.c
    lcode.c
    lcorolib.c
    lctype.c
    ldblib.c
    ldebug.c
    ldo.c
    ldump.c
    lfunc.c
    lgc.c
    linit.c
    liolib.c
    llex.c
    lmathlib.c
    lmem.c
    loadlib.c
    lobject.c
    lopcodes.c
    loslib.c
    lparser.c
    lstate.c
    lstring.c
    lstrlib.c
    ltable.c
    ltablib.c
    ltm.c
    lundump.c
    lutf8lib.c
    lvm.c
    lzio.c
)

TARGET_INCLUDE_DIRECTORIES(sharedlua PRIVATE .)

IF(WIN32)
    TARGET_COMPILE_DEFINITIONS(sharedlua PRIVATE LUA_BUILD_AS_DLL)
ENDIF()

ADD_CUSTOM_COMMAND(TARGET sharedlua POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    "$<TARGET_FILE:sharedlua>"
    "${CMAKE_BINARY_DIR}"
)
