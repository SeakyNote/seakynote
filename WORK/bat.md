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
