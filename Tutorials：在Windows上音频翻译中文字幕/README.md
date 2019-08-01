# 在Windows上把音频先翻译成英文字幕，再翻译成中文字幕

## 安装前准备下载及安装

1. 国外网----美国网络  [官网下载安装](https://www.expressvpn.com/)  **翻译全程必备连接**
2. python2安装  [官网下载安装](https://www.python.org/downloads/release/python-2716/)
3. Chocolatey安装  **用管理员权限的cmd或PowerShell安装**
4. git安装  **用管理员权限的PowerShell安装，命令用Chocolatey**
5. python中的模块安装：pip、autosub、python-qt5、fbs、requests、pysrt、googletrans  **用管理员权限的cmd安装，命令用pip**
6. FFMPEG文件下载  [官网下载](https://ffmpeg.zeranoe.com/builds/)
7. subtitle-translator软件下载安装  [Github下载安装](https://github.com/suifengtec/subtitle-translator/releases/tag/v1.0.0)


### 详解

1. 国外网----美国网络

	连接国外翻译资源库<br/>
	购买了ExpressVPN，稳定，安全，不用不行。<br/>
	文件：Windows桌面版：expressvpn_7.1.1.7992.exe
	
2. python2安装  **作为编程语言基础**

	安装过程中勾选在系统变量中添加上path路径。<br/>
	文件：python-2.7.16.amd64.msi

3. Chocolatey安装  **用于安装git**

	- 以管理员权限打开PowerShell，输入命令：<br/>
`Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`

	    或：以管理员权限打开cmd，输入命令：<br/>
`@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`

	- 测试：打开cmd或PowerShell，输入`choco`或`choco -?`，输出帮助信息
	- 升级Chocolatey命令：`choco upgrade chocolatey`

4. git安装  **Git Bash用于各种命令写入** 
<br/>（*Github安装<可暂时不安装>，安装教程：[Tutorials：在Windows上搭建git和Github环境](https://github.com/JoyceLiu-LQ/Summary/tree/master/Tutorials%EF%BC%9A%E5%9C%A8Windows%E4%B8%8A%E6%90%AD%E5%BB%BAgit%E5%92%8CGithub%E7%8E%AF%E5%A2%83)*）

	- 打开管理员权限PowerShell<br/>
	- 输入`choco install git -y`<br/>
	
5. python中的模块安装：pip、autosub、python-qt5、fbs、requests、pysrt、googletrans  **构建翻译功能的基础模块**

	- pip模块用于其他各种python模块的安装。

	- 确认pip是否安装：按Win+R，输入cmd，打开命令提示符(cmd)。输入`pip -V`，显示版本信息。<br/>
	     升级pip的命令：`python -m pip install -U pip`
	- 安装autosub：打开cmd，输入`pip install autosub`。<br/>该模块只在python2中。<br/>
	    如果已安装，需要先卸载，输入`pip uninstall autosub`
	     <br/>测试：<br/>在cmd中输入`autosub`，输出Error:You need to specify a source path.安装成功
	- 其他模块同样用pip安装。代码：<br/>`pip install 模块1 模块2 模块3 ......`
	- 用pip安装googletrans后<br/>
	     - 测试一：打开Git Bash，输入`translate -h`，正常时出现帮助信息。<br/>
	     - 测试二：翻译中文<br/>
	     
		    在cmd中输入代码:<br/>		
		    `translate -s en -d zh-CN 'hello'`		 
		    <br/>如果出现：
	        'ascii' codec can't encode characters in position 8-50: ordinal not in range<br/>
	        解决：<br/>
	        python没办法处理非ascii编码的，此时需要自己设置将python的默认编码，一般设置为utf8的编码格式。<br/>
	        在python的Lib\site-packages文件夹下新建一个sitecustomize.py，代码为：
	        
	        ```
           # encoding=utf8  
		    import sys  
		    reload(sys)  
		    sys.setdefaultencoding('utf8') 
            ```

		<br/> 保存后再次进行测试二。输出“你好”。
	
6. FFMPEG文件下载

	文件：最新的FFMPEG - 64位版本（格式.zip）

7. subtitle-translator软件下载安装 *需要Qt5等模块的安装*

    专门用于翻译英文字幕srt为中文字幕srt的软件<br/>
	文件：subtitleTranslatorSetup.exe




## 操作步骤

1. 修改autosub的名字和代码
    - 更改autosub名字为autosub_app.py
    - 修改autosub_app.py中代码
2. 添加ffmpeg.exe
    - 复制ffmpeg.exe到python根目录
3. 重启电脑
4. 测试
5. SENDTO轻松处理：每次运行直接右键要翻译的视频，点击发送到，AutoSub_En.bat
6. 打开subtitleTranslator，翻译srt文件


### 操作步骤详解：

1. 修改autosub的名字和代码
    - 更改autosub名字为autosub_app.py
	    - 运行cmd
	    - 输入命令：`rename C:\Python27\Scripts\autosub autosub_app.py`
    - 修改autosub_app.py中代码
	    - 使用Python IDLE 打开
	    - 第48行：<br/>
		`temp = tempfile.NamedTemporaryFile(suffix='.flac')`<br/>
	    变更为：
	    <br/>`temp = tempfile.NamedTemporaryFile(suffix='.flac', delete=False)`
	    - 第127行：<br/>
		`exe_file = os.path.join(path, program)`<br/>
	    变更为：
	    <br/>`exe_file = os.path.join(path, program + ".exe")`

2. 添加ffmpeg.exe

    - 解压文件ffmpeg.zip
    - 复制ffmpeg.exe到python根目录C:/Python27/

3. 重启Windows

4. 测试

    - 输入cmd命令：`C:\Python27\python.exe C:\Python27\scripts\autosub_app.py --list-languages`
    - 输出[语言代码: INFO-list_of_languages.txt](https://github.com/CaiNiaoManNonglqzhb/Summary-JoyceLiu/blob/master/Tutorials%EF%BC%9A%E5%9C%A8Windows%E4%B8%8A%E6%8A%8A%E9%9F%B3%E9%A2%91%E5%85%88%E7%BF%BB%E8%AF%91%E6%88%90%E8%8B%B1%E6%96%87%E5%AD%97%E5%B9%95%EF%BC%8C%E5%86%8D%E7%BF%BB%E8%AF%91%E6%88%90%E4%B8%AD%E6%96%87%E5%AD%97%E5%B9%95/INFO-list_of_languages.txt)

5. SENDTO轻松处理

    - Win+R，输入`shell:sendto`，打开“发送到”文件夹
    - 在文件夹下添加AutoSub_En.bat
	    - 在文件夹下右键，点击Git Bash，
	    - 输入`nano`，Ctrl+O保存为AutoSub_En.bat，（nano文本编辑器上快捷键请查看 [nano快捷键.txt](https://github.com/CaiNiaoManNonglqzhb/Summary-JoyceLiu/blob/master/Tutorials%EF%BC%9A%E5%9C%A8Windows%E4%B8%8A%E6%8A%8A%E9%9F%B3%E9%A2%91%E5%85%88%E7%BF%BB%E8%AF%91%E6%88%90%E8%8B%B1%E6%96%87%E5%AD%97%E5%B9%95%EF%BC%8C%E5%86%8D%E7%BF%BB%E8%AF%91%E6%88%90%E4%B8%AD%E6%96%87%E5%AD%97%E5%B9%95/nano%E5%BF%AB%E6%8D%B7%E9%94%AE.txt)）
	    - 输入命令：<br/>`C:\Python27\python.exe C:\Python27\Scripts\autosub_app.py -C 2 -S en -D en %1`   
            #### 注意：
            - en代表英语，不同的语言对应测试中list-languages中的语言代表，例如zh-CN代表中文简体
            - %1 代表视频，不可少
            - 源语言和目标语言是一致的
            - 生成同名srt文件

6. 打开subtitleTranslator，翻译srt文件<br/>
	Ctrl+F：查找/打开字幕文件，默认支持srt类型的字幕；<br/>
	Ctrl+T：翻译该字幕文件，如果没有选择语种的话，默认默认翻译为简体中文；<br/>
	Ctrl+S：保存翻译后的字幕文件；<br/>
	Ctrl+Alt+S：保存为双语种字幕文件。<br/>



