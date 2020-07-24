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
```json
// tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Build",  // 任务的名字叫Build，注意是大小写区分的，等会在launch中调用这个名字
            "type": "shell",  // 任务执行的是shell命令，也可以是
            "command": "g++", // 命令是g++
            "args": [
                "'-Wall'",
                "'-std=c++17'",  //使用c++17标准编译
                "'${file}'", //当前文件名
                "-o", //对象名，不进行编译优化
                "'${fileBasenameNoExtension}.exe'",  //当前文件名（去掉扩展名）
            ],
          // 所以以上部分，就是在shell中执行（假设文件名为filename.cpp）
          // g++ filename.cpp -o filename.exe
            "group": { 
                "kind": "build",
                "isDefault": true   
                // 任务分组，因为是tasks而不是task，意味着可以连着执行很多任务
                // 在build组的任务们，可以通过在Command Palette(F1) 输入run build task来运行
                // 当然，如果任务分组是test，你就可以用run test task来运行 
            },
            "problemMatcher": [
                "$gcc" // 使用gcc捕获错误
            ],
        }
    ]
}
```
