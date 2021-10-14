```bat
@echo off

rem 此脚本的文件格式为GBK2312格式，否则在中文环境下中文汉字会乱码

rem 更新代码
svn update

call "C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\vcvars32.bat"

:generate_resource
set build_resource=
set /p build_resource=是否编译代码，如果不需要重新编译，继续上次的编译版本，输入n即可（不编译请输入n，编译直接回车）： 
if not "%build_resource%" == "" ( if not "%build_resource%" == "n" ( goto generate_resource ) ) 
if "%build_resource%" == "n" ( goto build_code ) else ( goto build_resource )

:build_resource
call ./Tools/Publish/Scripts/generate_run_env.bat

:build_code
cd /d %~dp0

devenv project.sln /Build "Debug|Win32"

pause
```

