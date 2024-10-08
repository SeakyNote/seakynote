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
```
for /d /r %%i in (build) do (
    if exist "%%i" (
        rd /s /q "%%i"
    )
)
```

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

## bat mkdir报文件名、目录名或卷标语法不正确
set文件夹路径时等号前后不要有空格

## bat中cd /d作用
带/d可以切换当前驱动器，否则不能

## setlocal/endlocal作用
`setlocal` 和 `endlocal` 是批处理脚本中的命令，用于管理环境变量的范围和作用域。它们的主要作用如下：

### `setlocal`
`setlocal` 命令用于启动一个本地化的环境变量范围。它会保存当前的环境变量，并在脚本的这一部分执行过程中，所有对环境变量的修改都只在本地范围内有效。当执行 `endlocal` 时，所有在 `setlocal` 和 `endlocal` 之间的环境变量修改都会被撤销，环境变量恢复到 `setlocal` 之前的状态。

### `endlocal`
`endlocal` 命令用于结束一个由 `setlocal` 启动的本地化环境变量范围，并恢复环境变量到 `setlocal` 之前的状态。如果没有显式调用 `endlocal`，当批处理脚本结束时，环境变量也会自动恢复到 `setlocal` 之前的状态。

### 示例说明
在上述批处理脚本中使用 `setlocal` 和 `endlocal` 的作用是：

1. **隔离环境变量修改**：在 `setlocal` 和 `endlocal` 之间，对环境变量的任何修改（如 `set source` 和 `set destination`）都不会影响到脚本外的环境。这样可以避免污染或意外修改系统的环境变量。

2. **安全性**：确保在批处理脚本运行后，系统环境变量保持不变，这对于脚本在不同环境下的可靠运行很重要。

### 代码示例

```batch
@echo off
setlocal

REM 源文件夹（需要复制文件的文件夹）
set source=C:\path\to\source

REM 目标文件夹（复制到的文件夹）
set destination=C:\path\to\destination

REM 创建目标文件夹（如果不存在）
if not exist "%destination%" (
    mkdir "%destination%"
)

REM 使用 xcopy 复制文件和文件夹，排除指定的文件和文件夹
xcopy "%source%\*" "%destination%\" /E /I /EXCLUDE:exclude.txt

REM exclude.txt 文件内容（要排除的文件和文件夹）
(
    echo .git\
    echo .gitattributes
    echo .gitignore
    echo .gitmodules
) > exclude.txt

REM 删除临时的 exclude.txt 文件
del exclude.txt

endlocal
```

在这段代码中，`setlocal` 和 `endlocal` 的使用确保了 `source` 和 `destination` 的设置以及创建和删除 `exclude.txt` 文件的操作仅在本地范围内有效，不会影响到其他批处理脚本或系统环境。这样可以提高脚本的可靠性和可维护性。

## bat执行后，set变量还会保留吗？
在 Windows 上使用批处理（.bat）文件时，`set` 命令用于设置环境变量。默认情况下，当你在一个批处理文件中设置一个环境变量后，该变量的作用域仅限于该批处理文件的执行过程。一旦批处理文件执行完毕，这些变量将会消失，不会保留在调用该批处理文件的命令提示符会话中。

例如，假设你有一个名为 `example.bat` 的批处理文件，其中包含以下内容：

```bat
@echo off
set MY_VARIABLE=HelloWorld
echo %MY_VARIABLE%
```

当你执行 `example.bat` 时，它会输出 `HelloWorld`，但是执行完毕后，如果你在同一个命令提示符中输入 `echo %MY_VARIABLE%`，则不会显示任何内容，因为 `MY_VARIABLE` 变量已经消失了。

如果你希望环境变量在批处理文件执行完毕后仍然保留，可以在命令提示符中直接使用 `set` 命令，或者在批处理文件中调用 `cmd /k` 保持会话打开。例如：

```bat
@echo off
set MY_VARIABLE=HelloWorld
echo %MY_VARIABLE%
cmd /k
```

这样批处理文件执行完后，会打开一个新的命令提示符会话，并保留设置的环境变量。或者，你可以使用 `setx` 命令将环境变量永久地添加到系统环境中，不过这会影响所有后续的命令提示符会话和系统环境：

```bat
@echo off
setx MY_VARIABLE HelloWorld
```

请注意，`setx` 设置的变量需要重新打开命令提示符才会生效。

## bat批处理如何将某个目录下的文件及文件夹全部删除？
在 Windows 的批处理（batch script）文件中，你可以使用 `del` 命令和 `rd` 命令来删除指定目录下的所有文件和文件夹。以下是一个示例脚本，该脚本将删除指定目录下的所有文件和文件夹：

```batch
@echo off
setlocal

REM 设定要删除的目录路径
set TARGET_DIR=C:\path\to\directory

REM 删除目录中的所有文件
del /Q /F "%TARGET_DIR%\*"

REM 删除目录中的所有子文件夹及其内容
for /D %%p in ("%TARGET_DIR%\*") do rmdir /S /Q "%%p"

endlocal
```

以下是每个命令的详细说明：

1. `@echo off`：关闭命令回显。
2. `setlocal`：开始一个本地环境块，确保变量不影响到脚本外部。
3. `set TARGET_DIR=C:\path\to\directory`：设置一个变量 `TARGET_DIR` 为你要删除文件和文件夹的目录路径。
4. `del /Q /F "%TARGET_DIR%\*"`：删除 `TARGET_DIR` 目录下的所有文件。`/Q` 表示静默模式（不提示确认），`/F` 表示强制删除只读文件。
5. `for /D %%p in ("%TARGET_DIR%\*") do rmdir /S /Q "%%p"`：遍历 `TARGET_DIR` 目录下的所有子文件夹，并使用 `rmdir /S /Q` 删除这些文件夹。`/S` 表示递归删除文件夹及其内容，`/Q` 表示静默模式。
6. `endlocal`：结束本地环境块。

请确保在执行此脚本前备份重要数据，因为这将永久删除指定目录下的所有文件和文件夹。

## bat终止脚本但保留之前输出记录
在批处理文件（.bat）中，如果想终止脚本的执行但保留之前的输出记录，你可以使用以下几种方法：

### 1. 使用 `goto` 指令
你可以使用 `goto` 指令将执行跳转到脚本的末尾，从而停止脚本的进一步执行，但保留之前的输出。

```batch
echo This will be executed
goto :EOF  (or goto :end if you have a label named :end)
echo This will NOT be executed

:end
```

`goto :EOF` 会直接跳转到脚本的结尾，而不再执行后续的命令。

### 2. 使用 `exit /B` 指令
你可以使用 `exit /B` 退出当前批处理脚本或子程序，而不关闭整个命令行窗口。

```batch
echo This will be executed
exit /B
echo This will NOT be executed
```

这样做也会保留之前的输出，但终止了脚本的进一步执行。

### 3. 使用 `rem` 或 `::` 注释掉后续命令
你还可以选择简单地注释掉你不想执行的部分：

```batch
echo This will be executed
rem echo This will NOT be executed

:: Another way to comment
:: echo This will NOT be executed
```

以上这些方法都可以有效地终止批处理脚本的执行，同时保留之前的输出记录。

