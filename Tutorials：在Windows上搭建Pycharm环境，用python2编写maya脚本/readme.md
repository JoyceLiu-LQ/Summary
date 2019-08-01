# 搭建Pycharm环境，用python2编写maya脚本

## 安装前软件工具等准备

1. 安装python2.7.16   
 [官网下载安装](https://www.python.org/downloads/release/python-2716/)

2. 安装maya2019，激活

3. 安装Pycharm2019.1<br/>
 [官网下载安装](https://www.jetbrains.com/pycharm/download/#section=windows)
 选择社区版即可

4. 下载maya官方devkit文件夹<br/>
 [官网下载地址]( https://www.autodesk.com/developer-network/platform-technologies/maya)
 页面最底部下载devkit文件对应版本
 
 
## 详细步骤
1. 为Pycharm添加mayapy.exe解析器<br/>
  file-seting-project:"新建的项目名称"-project interpreter-"下拉框或者是齿轮图标"-show all-点击“+”号-virtualenv environment-Existing environment-点击省略号-找到路径(C:\Program Files\Autodesk\Maya2019\bin\mayapy.exe)-点击应用后逐个点击确定 - 下方会出现install提示，点击install并安装插件

2. Pycharm安装mayacharm插件<br/>
  file-seting-plugin-安装mayacharm插件
  
3. 正确放置devkit文件夹用于开发<br/>
  解压devkit文件，将整个文件夹放置在maya2019根目录下

4. Windows中添加Maya的Path路径<br/>
  文件资源管理器-属性-高级系统设置-环境变量-系统变量-“path”-编辑-点击“新建”-（C:\Program Files\Autodesk\Maya2019\bin） 

5. 给“mayapy.exe”解析器添加一个路径并删除一个路径<br/>
  file-seting-project:"新建的项目名称"-project interpreter-show all-选中“mayapy.exe”解析器-点击右侧最后一个图标（按钮名称为"show paths for selected interpreter“）-点击“+”号-添加("C:\Program Files\Autodesk\Maya2019\devkitBase\devkit\other\pymel\extras\completion\py")路径，同时删除（”.......Lib\site-packegs“）路径，确定后重启 pycharm ! ! !
  
6. 用代码连接Pycharm到maya<br/>
  file-seting-mayacharm-双击（“4434路径”）- 文字复制框中“端口代码”到maya-python窗口-点击上方三角形运行，链接成功
    #### 端口代码
    ```
    import maya.cmds as cmds

    if not cmds.commandPort(':4434', query=True):
        cmds.commandPort(name=':4434')
     ```


## 测试

1. file-seting-project:"新建的项目名称"-project interpreter-更改解析器为“mayapy.exe”

2. 右上角下拉菜单configuration-点击“+”号-选择mayacharm插件-右侧file框中找到当前python文件路径-修改最上方“name”为"maya2019"-应用并确定

3. 在项目中新建python文件，输入代码：
    ```
    import maya.cmds as cmds
    cmds.polySphere()
    ```
    在maya中出现一个球。