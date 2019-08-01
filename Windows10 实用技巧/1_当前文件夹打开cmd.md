# 在当前文件夹打开cmd。

 在当前文件夹上 按住Shift键点击右键，同时显示“在此处打开命令窗口”和“在此处打开Powershell窗口”两个选项


### windows10右键添加“在此处打开命令窗口”：*安装git之后*

1. 在桌面右键Git Bash，输入`nano`，Ctrl+O命名文件名称为OpenCmdHere.reg

2. 输入代码：
```
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\Directory\shell\OpenCmdHere] 
@="在此处打开命令窗口" "Icon"="cmd.exe" 

[HKEY_CLASSES_ROOT\Directory\shell\OpenCmdHere\command] 
@="cmd.exe /s /k pushd "%V"" 

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCmdHere] 
@="在此处打开命令窗口" "Icon"="cmd.exe" 

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCmdHere\command] 
@="cmd.exe /s /k pushd \"%V\"" 

[HKEY_CLASSES_ROOT\Drive\shell\OpenCmdHere] 
@="在此处打开命令窗口" "Icon"="cmd.exe" 

[HKEY_CLASSES_ROOT\Drive\shell\OpenCmdHere\command] 
@="cmd.exe /s /k pushd \"%V\"" 

[HKEY_CLASSES_ROOT\LibraryFolder\background\shell\OpenCmdHere] 
@="在此处打开命令窗口" "Icon"="cmd.exe" 

[HKEY_CLASSES_ROOT\LibraryFolder\background\shell\OpenCmdHere\command]
@="cmd.exe /s /k pushd \"%V\""

```

3. 保存后双击运行。
