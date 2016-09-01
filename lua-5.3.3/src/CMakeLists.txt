set(LUA_NAME ${PROJECT_NAME})
set(LUA_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(LUA_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${LUA_INCLUDE_DIR})
set(LUA_INCLUDE_FILES
        lapi.h
        lauxlib.h
        lcode.h
        lctype.h
        ldebug.h
        ldo.h
        lfunc.h
        lgc.h
        llex.h
        llimits.h
        lmem.h
        lobject.h
        lopcodes.h
        lparser.h
        lprefix.h
        lstate.h
        lstring.h
        ltable.h
        ltm.h
        lua.h
        lua.hpp
        luaconf.h
        lualib.h
        lundump.h
        lvm.h
        lzio.h
        )

set(LUA_SRC_FILES
        lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c
        lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c
        lparser.c lstate.c lstring.c ltable.c ltm.c
        lundump.c lvm.c lzio.c lauxlib.c lbaselib.c
        lbitlib.c lcorolib.c ldblib.c liolib.c lmathlib.c
        loslib.c lstrlib.c ltablib.c lutf8lib.c loadlib.c
        linit.c
        )
set(LUA_EXE_SRC lua.c)
set(LUAC_EXE_SRC luac.c)

set_property(GLOBAL PROPERTY LUA_INCLUDE_DIR ${LUA_INCLUDE_DIR})
set_property(GLOBAL PROPERTY LUA_NAME ${LUA_NAME})

add_library(${LUA_NAME}s STATIC ${LUA_SRC_FILES})
set_target_properties(${LUA_NAME}s PROPERTIES OUTPUT_NAME ${LUA_NAME})
target_link_libraries(${LUA_NAME}s m)

#lua
add_executable(lua ${LUA_EXE_SRC})
target_link_libraries(lua ${LUA_NAME}s)

#luac
add_executable(luac ${LUAC_EXE_SRC})
target_link_libraries(luac ${LUA_NAME}s)


install(TARGETS ${LUA_NAME}s  LIBRARY DESTINATION ${PROJECT_BINARY_DIR}/lib ARCHIVE DESTINATION ${PROJECT_BINARY_DIR}/lib)
#install(TARGETS ${LUA_NAME}  LIBRARY DESTINATION ${PROJECT_BINARY_DIR}/lib ARCHIVE DESTINATION ${PROJECT_BINARY_DIR}/lib)
install(FILES  ${LUA_INCLUDE_FILES}  DESTINATION ${PROJECT_BINARY_DIR}/include/lua)

install(TARGETS lua RUNTIME DESTINATION ${PROJECT_BINARY_DIR}/bin BUNDLE DESTINATION ${PROJECT_BINARY_DIR}/bin)
install(TARGETS luac RUNTIME DESTINATION ${PROJECT_BINARY_DIR}/bin BUNDLE DESTINATION ${PROJECT_BINARY_DIR}/bin)
