# 声明

本项目纯粹是个人兴趣基于官方main分支做的修改，肯定存在不足之处，如果有疑问欢迎issue交流。
后续不一定会持续跟进，请以官方版本为准。

# 环境说明

* Visual Studio 2022 Community
* msys2
* go 1.22
* [ilogtail-windows](https://github.com/leejoker/ilogtail-windows)
* [ilogtail-deps](https://ilogtail-community-edition.oss-cn-shanghai.aliyuncs.com/prebuilt-dependencies/ilogtail-deps.windows-x64.zip)
* [boost_1_68](https://ilogtail-community-edition.oss-cn-shanghai.aliyuncs.com/prebuilt-dependencies/boost_1_68_0-msvc-14.1-64.exe)
* [protobuf v3.7.1](https://github.com/protocolbuffers/protobuf/tree/v3.7.1) 用于替换ilogtail-deps中的include和lib
* [cmake](https://github.com/Kitware/CMake/releases/download/v3.29.2/cmake-3.29.2-windows-x86_64.zip)

# 步骤说明

1. 编译protobuf

```shell
git clone https://github.com/protocolbuffers/protobuf.git
git checkout v3.7.1
git submodule update --init --recursive
```

使用cmake-gui转换为当前Visual Studio的项目，然后进行编译。

2. 替换ilogtail-deps

使用Release目录下的lib文件替换ilogtail-deps\lib目录下的同名文件。
使用protobuf\src\google目录替换ilogtail-deps/include中的同名目录
使用protobuf\third_party\googletest\googletest\include\gtest替换ilogtail-deps/include中的同名目录

3. 根据[官方文档](https://ilogtail.gitbook.io/ilogtail-docs/installation/sources/build)替换windows64_build.bat中的变量
4. 执行编译脚本
5. 如果遇到RuntimeLibrary报错问题，请将按照以下进行替换，重新编译：
```xml
<RuntimeLibrary>MultiThreadedDLL</RuntimeLibrary>
```
替换为：
```xml
<RuntimeLibrary>MultiThreaded</RuntimeLibrary>
```
然后执行后续插件编译部分的脚本即可。