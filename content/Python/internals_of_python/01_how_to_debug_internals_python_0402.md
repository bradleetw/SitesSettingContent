---
title: "如何設定 VSCode c/c++ 開發環境(macOS) - internals of python "
date: 2019-04-02T08:58:15+08:00
draft: true
tags:
categories:
authors: ["bradlee"]
toc: false
mathjax: false
---

## VSCode

VSCode 是 Microsoft 主導的開源文檔編輯器, 或許說是整合開發環境(IDE), 但不提供預設的編譯功能(是有提供基本的編譯功能), 所以可以讓使用者自行設定關聯各式各樣的編譯器, e.g. gcc, python... .

VSCode 可以在 Micorsoft Windows 10, MacOS, and Linux 等平台上執行, 原理應是 VSCode 基於 Electron(基於 Chromium) 開發.

<https://zh.wikipedia.org/wiki/Visual_Studio_Code>

### 下載安裝 VSCode

下載網頁, <https://code.visualstudio.com/>.

可參考其他開發者的安裝經驗 
<https://ithelp.ithome.com.tw/articles/10195139>
[在linux上安装VSCode](<https://www.jianshu.com/p/9387d192f377>)
[在 CentOS 7 安裝 VSCode](<https://ephrain.net/vscode-%E5%9C%A8-centos-mac-windows-%E4%B8%8A%E5%AE%89%E8%A3%9D-visual-studio-code/>)
[VS Code安装、配置、使用（windows10 64）](<https://blog.csdn.net/HelloZEX/article/details/84029810>)
[VSCode 布道指南 V1.0 (一)](<https://zhuanlan.zhihu.com/p/44593798>)

### 安裝相關的 Extensions

在 VSCode Extensions: Marketplace 有各類豐富的插件, 針對 C/C++ 的開發環境, 安裝

1. C/C++ - from Microsoft. <https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools>

2. C/C++ Clang Command Adapter <https://marketplace.visualstudio.com/items?itemName=mitaki28.vscode-clang>

這兩個提供編輯 C/C++ 時, 即時的診斷和提示, 和 Debug 功能.

在 settings.json 中加入如下設定

```json
    "C_Cpp.updateChannel": "Insiders",
    "C_Cpp.autocomplete": "Disabled",
    "clang.cxxflags": [
        "-std=c++14",
        "-std=c11",
        "-Wall"
    ]
```

[Visual Studio Code 如何编写运行 C、C++ 程序？](<https://www.zhihu.com/question/30315894>)

### 設定 Build, Debug, and IntelliSense

主要增加修改 3 個在 `.vscode` 的 json file:

1. tasks.json
2. launch.json
3. c_cpp_properties.json

相關的設定參考 [Visual Studio Code 如何编写运行 C、C++ 程序？](<https://www.zhihu.com/question/30315894>)

#### tasks.json

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Run tests",
            "type": "shell",
            "command": "./scripts/test.sh",
            "windows": {
                "command": ".\\scripts\\test.cmd"
            },
            "group": "test",
            "presentation": {
                "reveal": "always",
                "panel": "new"
            }
        }
    ]
}
```

The task's properties have the following semantic:

- **label**: The task's label used in the user interface.
- **type**: The task's type. For a custom task, this can either be `shell` or `process`. If `shell` is specified, the command is interpreted as a shell command (for example: bash, cmd, or PowerShell). If process is specified, the command is interpreted as a process to execute.
- **command**: The actual command to execute.
- **windows**: Any Windows specific properties. Will be used instead of the default properties when the command is executed on the Windows operating system.
- **group**: Defines to which group the task belongs. In the example, it belongs to the `test` group. Tasks that belong to the test group can be executed by running **Run Test Task** from the **Command Palette**.
- **presentation**: Defines how the task output is handled in the user interface. In this example, the Integrated Terminal showing the output is `always` revealed and a `new` terminal is created on every task run.
- **options**: Override the defaults for `cwd` (current working directory), `env` (environment variables), or `shell` (default shell). Options can be set per task but also globally or per platform. Environment variables configured here can only be referenced from within your task script or process and will not be resolved if they are part of your args, command, or other task attributes.
- **runOptions**: Defines when and how a task is run.

[Check more from schema of task.json.](<https://code.visualstudio.com/docs/editor/tasks-appendix>)

##### Compound tasks

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Client Build",
            "command": "gulp",
            "args": ["build"],
            "options": {
                "cwd": "${workspaceRoot}/client"
            }
        },
        {
            "label": "Server Build",
            "command": "gulp",
            "args": ["build"],
            "options": {
                "cwd": "${workspaceRoot}/server"
            }
        },
        {
            "label": "Build",
            "dependsOn": ["Client Build", "Server Build"]
        }
    ]
}
```

If you list more than one task in the `dependsOn` property, they are executed in **parallel**.

Q: How to set the squential order of multi-tasks?

[Integrate with External Tools via Tasks](<https://code.visualstudio.com/docs/editor/tasks#vscode>)

[Variables Reference](<https://code.visualstudio.com/docs/editor/variables-reference>)

#### launch.json

[Debugging](<https://code.visualstudio.com/docs/editor/debugging#_launch-configurations>)

[Launch.json attributes](<https://code.visualstudio.com/docs/editor/debugging#_launchjson-attributes>)

#### c_cpp_properties.json

`c_cpp_properties.json` to specify the compiler path.

[Configure the compiler path](<https://code.visualstudio.com/docs/cpp/config-clang-mac#_configure-the-compiler-path>)

## Internals of python

### 下載 Python source code

### 設定相關編譯 python 所需要的環境變數

### 在 Command line 下編譯 python

### 在 VSCode 中編譯 python

### 在 VSCode 中 debug

## Reference

https://lldb.llvm.org/lldb-gdb.html

https://hackmd.io/s/ByMHBMjFe
https://akaptur.com/blog/2014/08/03/getting-started-with-python-internals/
https://akaptur.com/blog/2014/06/11/of-syntax-warnings-and-symbol-tables/


https://segmentfault.com/a/1190000004136351
https://blog.csdn.net/wj1066/article/details/83653153

https://dawranliou.com/blog/2017/02/20/getting-started-python-internals.html
https://eli.thegreenplace.net/2015/the-scope-of-index-variables-in-pythons-for-loops/
https://eli.thegreenplace.net/2012/03/23/python-internals-how-callables-work
https://eli.thegreenplace.net/2010/06/30/python-internals-adding-a-new-statement-to-python/

<https://github.com/Junnplus/blog/projects/1>

<https://zhuanlan.zhihu.com/p/22275595>

<https://www.zhihu.com/question/29372574/answer/88624507>

<http://aosabook.org/en/index.html>

<http://aosabook.org/en/500L/a-python-interpreter-written-in-python.html>


