# CMakeLists.txt in the "lua" directory
cmake_minimum_required(VERSION 3.16)


# Lua source files
set(LUA_SRC
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
    lua.c
    lundump.c
    lutf8lib.c
    lvm.c
    lzio.c
)

set(LUA_HEADER
    lapi.h
    lauxlib.h
    lcode.h
    lctype.h
    ldebug.h
    ldo.h
    lfunc.h
    lgc.h
    ljumptab.h
    llex.h
    llimits.h
    lmem.h
    lobject.h
    lopcodes.h
    lopnames.h
    lparser.h
    lprefix.h
    lstate.h
    lstring.h
    ltable.h
    ltests.h
    ltm.h
    lua.h
    luaconf.h
    lualib.h
    lundump.h
    lvm.h
    lzio.h
)

list(APPEND LUA_SRC ${LUA_HEADER})

add_library(Lua ${LUA_SRC})

target_include_directories(Lua
 PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/..
)

target_compile_definitions(Lua PUBLIC $<$<CONFIG:Debug>:LUA_DEBUG>)

if(WINDOWS)
  target_compile_definitions(Lua PRIVATE LUA_BUILD_AS_DLL)
elseif(MACOSX)
  target_compile_definitions(Lua PUBLIC LUA_USE_MACOSX)
elseif(UNIX)
    target_compile_definitions(Lua PUBLIC LUA_USE_LINUX)
endif()

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${LUA_SRC})