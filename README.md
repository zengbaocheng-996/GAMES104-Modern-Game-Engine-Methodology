# GAMES104-Modern-Game-Engine-Methodology

| Index | English                    | 中文                  |
| ----- | -------------------------- | --------------------- |
| 01    | Build and Run Pilot Engine | 编译和运行 Pilot 引擎 |
| 02    | Rendering                  | 渲染                  |
| 03    | Animation and Physics      | 动画和物理            |
| 04    | Tool Chains                | 工具链                |
| 05    | C++ Call Lua               | 每帧执行 Lua 脚本     |
| 06    | Reflection System          | 反射系统              |
| 07    | Render System              | 渲染系统              |

### 代码结构

| .\                                                           | 目的                              |
| ------------------------------------------------------------ | --------------------------------- |
| build                                                        | cmake . -B build 后生成的工程     |
| .github<br />.gitlab<br />.clang-format<br />.clang-tidy<br />.gitignore | 各个工具配置文件                  |
| cmake<br />CMakeLists.txt                                    | \                                 |
| scripts<br />build_linux.sh<br />build_macos.sh<br />build_windows.bat | 批处理文件 方便构建引擎编写的脚本 |
| LICENSE<br />README.md<br />ReleaseNotes.md                  | \                                 |
| engine (如下表)                                              | \                                 |

| .\engine\                  | 目的                                                     |
| -------------------------- | -------------------------------------------------------- |
| 3rdparty                   | 第三方库或二进制库                                       |
| asset                      | 引擎启动默认关卡需要的组成                               |
| bin<br />bin\PiccoloParser | 构建过程生成<br />解析C++代码 根据模板文件生成功能性代码 |
| configs                    | 编辑器启动时所需配置文件                                 |
| jolt-asset                 | 物理库 Jolt Physics 所需 Shader                          |
| shader                     | 引擎启动必须运行的 Shader                                |
| template                   | 模板文件 对应 PiccoloParser                              |
| .gitignore                 | 指定不加入版本仓库的文件                                 |
| CMakeList.txt              | 指明工程是如何构建的                                     |
| source (如下表)            | \                                                        |

| .\engine\source\ | 目的                                                         |
| ---------------- | ------------------------------------------------------------ |
| _generated       | 引擎生成所需功能性代码                                       |
| editor           | 编辑器源代码                                                 |
| meta_parser      | PiccoloParser 源代码                                         |
| precompile       | CMake 脚本和配置文件 引擎构建前命令 PiccoloParse 解析源代码 生成所需功能性代码 |
| .gitignore       | 指定不加入版本仓库的文件                                     |
| text             | 单元测试和其他测试代码                                       |
| runtime (如下表) | 引擎核心                                                     |

| .\engine\source\runtime\ | 目的                      |
| ------------------------ | ------------------------- |
| CMakeLists.txt           | 指定 runtime 工程如何构建 |
| engine.cpp<br />engine.h | 引擎入口                  |
| function                 | Function Layer            |
| resource                 | Resource Layer            |
| core                     | Core Layer                |
| platform                 | Platform Layer            |

