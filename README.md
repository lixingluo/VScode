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
```
// launch.json
{
    "version": "0.2.0",
    "configurations": [
        {
            // this name is same as RUN 
            "name": "g++-10 - Build and debug active file",
            // this name is same as tasks.label in tasks.json
            "preLaunchTask": "C/C++: g++-10 build active file",
            "type": "cppdbg",
            "request": "launch",
            // executable file, current folder/current file name without extension
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            // choose true will stop the program after console opened, not execute program directly
            "stopAtEntry": false,
            // current working path: the working space folder of current file 
            "cwd": "${workspaceFolder}",
            "environment": [],
            // if change to false, then will call terminal
            "externalConsole": false,
            "MIMode": "lldb"
        }]
}
```
## 三. VSCode预定义变量中文详解和示例
### 预定义变量
- ${workspaceFolder} - 当前工作目录(根目录)
- ${workspaceFolderBasename} - 当前文件的父目录
- ${file} - 当前打开的文件名(完整路径)
- ${relativeFile} - 当前根目录到当前打开文件的相对路径(包括文件名)
- ${relativeFileDirname} - 当前根目录到当前打开文件的相对路径(不包括文件名)
- ${fileBasename} - 当前打开的文件名(包括扩展名)
- ${fileBasenameNoExtension} - 当前打开的文件名(不包括扩展名)
- ${fileDirname} - 当前打开文件的目录
- ${fileExtname} - 当前打开文件的扩展名
- ${cwd} - 启动时task工作的目录
- ${lineNumber} - 当前激活文件所选行
- ${selectedText} - 当前激活文件中所选择的文本
- ${execPath} - vscode执行文件所在的目录
- ${defaultBuildTask} - 默认编译任务(build task)的名字
### 预定义变量示例
####  _假设你满足以下的条件_
1. 一个文件/home/your-username/your-project/folder/file.ext在你的编辑器中打开
2. 一个目录/home/your-username/your-project作为你的根目录
####  _预定义变量则是_
- ${workspaceFolder} - /home/your-username/your-project
- ${workspaceFolderBasename} - your-project
- ${file} - /home/your-username/your-project/folder/file.ext
- ${relativeFile} - folder/file.ext
- ${relativeFileDirname} - folder
- ${fileBasename} - file.ext
- ${fileBasenameNoExtension} - file
- ${fileDirname} - /home/your-username/your-project/folder
- ${fileExtname} - .ext
- ${lineNumber} - 光标所在行
- ${selectedText} - 编辑器中所选择的文本
- ${execPath} - Code.exe的位置
