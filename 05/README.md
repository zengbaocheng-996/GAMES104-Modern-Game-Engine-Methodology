# C++ Call Lua

| 第三方库 | 下载地址                                           |
| -------- | -------------------------------------------------- |
| Lua      | https://github.com/lua/lua/releases/tag/v5.4.4     |
| Sol      | https://github.com/ThePhD/sol2/releases/tag/v3.3.0 |

###### cmake 编译运行指令

```shell
cmake -Bbuild
cmake --build build
```

###### engine/3rdparty/lua.cmake

Windows 没有 grep 指令 VSCode Alt+左键手动整理

```shell
ls | findstr ".c" > grep.txt
```

```cmake
set(lua_SOURCE_DIR_ ${CMAKE_CURRENT_SOURCE_DIR}/lua-5.4.4)
add_library(lua_static STATIC
${lua_SOURCE_DIR_}/lapi.c
${lua_SOURCE_DIR_}/lauxlib.c
${lua_SOURCE_DIR_}/lbaselib.c
${lua_SOURCE_DIR_}/lcode.c
${lua_SOURCE_DIR_}/lcode.h
${lua_SOURCE_DIR_}/lcorolib.c
${lua_SOURCE_DIR_}/lctype.c
${lua_SOURCE_DIR_}/lctype.h
${lua_SOURCE_DIR_}/ldblib.c
${lua_SOURCE_DIR_}/ldebug.c
${lua_SOURCE_DIR_}/ldo.c
${lua_SOURCE_DIR_}/ldump.c
${lua_SOURCE_DIR_}/lfunc.c
${lua_SOURCE_DIR_}/lfunc.h
${lua_SOURCE_DIR_}/lgc.c
${lua_SOURCE_DIR_}/lgc.h
${lua_SOURCE_DIR_}/linit.c
${lua_SOURCE_DIR_}/liolib.c
${lua_SOURCE_DIR_}/llex.c
${lua_SOURCE_DIR_}/lmathlib.c
${lua_SOURCE_DIR_}/lmem.c
${lua_SOURCE_DIR_}/loadlib.c
${lua_SOURCE_DIR_}/lobject.c
${lua_SOURCE_DIR_}/lobject.h
${lua_SOURCE_DIR_}/lopcodes.c
${lua_SOURCE_DIR_}/lopcodes.h
${lua_SOURCE_DIR_}/loslib.c
${lua_SOURCE_DIR_}/lparser.c
${lua_SOURCE_DIR_}/lstate.c                                                          
${lua_SOURCE_DIR_}/lstring.c                                                             
${lua_SOURCE_DIR_}/lstrlib.c                                                             
${lua_SOURCE_DIR_}/ltable.c                                                              
${lua_SOURCE_DIR_}/ltablib.c                                                             
# ${lua_SOURCE_DIR_}/ltests.c                                                             
${lua_SOURCE_DIR_}/ltm.c                                                                 
# ${lua_SOURCE_DIR_}/lua.c                                                               
${lua_SOURCE_DIR_}/luaconf.h                                                             
${lua_SOURCE_DIR_}/lundump.c                                                             
${lua_SOURCE_DIR_}/lutf8lib.c                                                             
${lua_SOURCE_DIR_}/lvm.c                                                                 
${lua_SOURCE_DIR_}/lzio.c                                                                 
# ${lua_SOURCE_DIR_}/onelua.c                                                            
)                                               
target_include_directories(lua_static PUBLIC ${lua_SOURCE_DIR_})
```

###### engine/3rdparty/CMakeLists.txt

```cmake
...
if(NOT TARGET sol2)
    add_subdirectory(sol2-3.3.0)
endif()
if(NOT TARGET lua)
    include(lua.cmake)
endif()
```

###### engine/source/runtime/CMakeLists.txt

```cmake
# Link dependencies
...
target_link_libraries(${TARGET_NAME} PUBLIC lua_static sol2)
```

###### engine/source/function/framework/component/lua/lua_component.cpp

```cpp
#include "runtime/function/framework/object/object.h"
#include "runtime/function/framework/component/lua/lua_component.h"
#include "runtime/core/base/macro.h"
namespace Piccolo
{
    void LuaComponent::postLoadResource(std::weak_ptr<GObject> parent_object)
    {
        m_parent_object = parent_object;
        m_lua_state.open_libraries(sol::lib::base);
    }
    void LuaComponent::tick(float delta_time)
    {
        // LOG_INFO(m_lua_script);
        m_lua_state.script(m_lua_script);
    }
} // namespace Piccolo
```

###### engine/source/function/framework/component/lua/lua_component.h

```c++
#pragma once
#include "sol/sol.hpp"
#include "runtime/function/framework/component/component.h"
namespace Piccolo
{
    REFLECTION_TYPE(LuaComponent)
    CLASS(LuaComponent : public Component, WhiteListFields)
    {
        REFLECTION_BODY(LuaComponent)
            
    public:
        LuaComponent() = default;
        void postLoadResource(std::weak_ptr<GObject> parent_object) override;
        void tick(float delta_time) override;

    protected:
        sol::state m_lua_state;
        META(Enable)
        std::string m_lua_script;
    };
} // namespace Piccolo
```

###### engine/asset/objects/character/player/player.object.json

```json
...
{
	"$context": {
	"lua_script": "print(\"c++ call lua\")"
	},
	"$typeName": "LuaComponent"
}
...
```

