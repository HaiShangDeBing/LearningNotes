# Visual Studio Code

## C/C++ 编程

**安装 Microsoft C/C++ extension:**

- 打开 VS Code.
- 点击侧栏的扩展按钮.
- 搜索 C++.
- 点击安装，然后重新加载.

 这个扩展不包含 C ++ 编译器或调试器。所以需要安装或使用计算机上已安装的编译调试工具。流行的 C ++ 编译器是 Windows 的 [MinGW](http://www.mingw.org/)，MacOS 的 [XCode](https://developer.apple.com/xcode/) 和 Linux 上的 [GCC](https://gcc.gnu.org/)。

**生成一个 c_cpp_properties.json 文件**

```json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceRoot}",
                "C:/MinGW/lib/gcc/mingw32/6.3.0/include/c++",
                "C:/MinGW/lib/gcc/mingw32/6.3.0/include/c++/mingw32",
                "C:/MinGW/lib/gcc/mingw32/6.3.0/include/c++/backward",
                "C:/MinGW/lib/gcc/mingw32/6.3.0/include",
                "C:/MinGW/lib/gcc/mingw32/6.3.0/include-fixed",
                "C:/MinGW/lib/gcc/mingw32/6.3.0/../../../../include"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE"
            ],
            "intelliSenseMode": "msvc-x64",
            "browse": {
                "path": [
                    "${workspaceRoot}",
                    "C:/MinGW/lib/gcc/mingw32/6.3.0/include/c++"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": ""
            },
            "cStandard": "c11",
            "cppStandard": "c++17"
        }
    ],
    "version": 3
}
```

不知道 include 路径有哪些，可以在 CMD 窗口使用 `gcc -v -E -x c++ -`。

**生成一个 tasks.json 文件构建应用程序**

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "type": "process",
            "command": "g++",
            "args": [
                "-g",
                "helloworld.cpp"
            ],
            "problemMatcher": [
                "$gcc"
            ]
        }
    ]
}
```

**生成一个 launch.json 文件启用调试**

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "C++ Launch (GDB)",
            "type": "cppdbg",
            "request": "launch",
            "preLaunchTask": "build",					
            "program": "${workspaceRoot}\\a.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceRoot}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "C:\\MinGW\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```

