## bat删文件
```bat
@REM 文件保留cad.bat start.bat README.md delete.bat
for /f %%i in ('dir /b /a-d *') do (
    if %%i neq cad.bat if %%i neq start.bat if %%i neq README.md if %%i neq delete.bat (
        del /f /s /q %%i
    )
)
@REM 文件夹保留bin
for /f %%i in ('dir /b /ad *') do (
    if %%i neq bin (
        rd /s /q %%i
    )
)

cd bin
@REM 仅保留文件夹testFolder
for /f %%i in ('dir /b /a-d *') do (
    del /f /s /q %%i
)

for /f %%i in ('dir /b /ad *') do (
    if %%i neq testFolder (
        rd /s /q %%i
    )
)

cd testFolder
@REM 文件夹不删除，文件保留testAppd.exe和所有dll文件
for /f %%i in ('dir /b /a-d *') do (
    if %%i neq testAppd.exe if %%~xi neq .dll (
        del /f /s /q %%i
    )
)
@REM 文件夹仅保留testFolder2
for /f %%i in ('dir /b /ad *') do (
    if %%i neq testFolder2 (
        rd /s /q %%i
    )
)

del %0
```

## 任务栏调用bat

https://www.win7zhijia.cn/win10jc/win10_30805.html

注意要调用的bat需要先cd到对应目录

## bat打开文件
```bat
start C:\XXX\XXX.txt

exit
```

## bat调bat

https://blog.csdn.net/yxzone/article/details/123817835

## 命令行输出所有目录

dir /B

## cmd获得目录下所有文件

dir /b /s /a-d

## bat递归删除目录下的build文件夹

如果你希望删除特定目录下，包括子目录中所有名称为 "build" 的文件夹，可以使用适当的批处理命令。以下是一个示例：

for /d /r %%i in (build) do (
    if exist "%%i" (
        rd /s /q "%%i"
    )
)
在这个修改后的脚本中：

for /d /r %%i in (build) 将会递归遍历当前目录及其所有子目录中所有名称为 "build" 的文件夹。
if exist "%%i" 确保只有存在的文件夹才会执行删除操作。
rd /s /q "%%i" 删除当前循环到的文件夹 %%i 及其所有内容，包括子目录中的同名文件夹。
这样修改后的脚本将删除指定目录及其所有子目录中所有名称为 "build" 的文件夹。请确保在运行这样的删除操作之前备份重要数据，以免数据丢失。

## bat复制文件例子

set fromDir = %ENV_VALUE\aaa\bbb
set toDir = %~dp0\..\ccc
xcopy "%fromDir%\*.dll" "%toDir%" /S /Y
xcopy "%fromDir%\eee.exe" "%toDir%" /Y
