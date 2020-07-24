# Mac VScode C++ 配置
## 目录
1. 有用的插件(Extensions)
2. tasks.json和launch.json配置详解
3. VSCode预定义变量中文详解和示例
## 一. 有用的插件(Extensions)
1. [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
2. [Native Debug](https://marketplace.visualstudio.com/items?itemName=webfreak.debug)
3. [C/C++ Compile Run](https://marketplace.visualstudio.com/items?itemName=danielpinto8zz6.c-cpp-compile-run)
## 二. tasks.json和launch.json配置详解
1. tasks.json用于编译source code生成byte codes
2. launch.json用于运行byte codes将运行结果输出到控制台
```
// tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            // tasks.label in tasks.json == configurations.preLaunchTask in launch.json
            "label": "C/C++: g++-10 build active file",
            // task run in the terminal is using shell command
            "type": "shell",
            // shell command is g++, /usr/local/bin/g++-10 is my g++ absolute path
            "command": "/usr/local/bin/g++-10",
            "args": [
                "-g",
                // current file name
                "${file}",
                // generate .out executable file
                "-o",
                // current folder name/current file name without extension - final generate excutable file location and its name
                "${fileDirname}/${fileBasenameNoExtension}",
            ],
            // since it's tasks.json not task.json, it can execute more than one task at a time
            // through run build task in Command Palette(F1)
            "group": {
                // if kind name is build, run build task; if kind name is test, run test task 
                "kind": "build",
                "isDefault": true
            },
            // use gcc catch error / debug
            "problemMatcher": [
                "$gcc"
            ],
        }
    ]
}
```
