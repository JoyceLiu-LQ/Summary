#  在Windows上搭建git和Github环境

*git可以轻松拥有无限个分支,Git是一款分布式版本控制系统,Git可以让团队更加高效的协同工作,提高工作效率,也不会因为频繁遭遇提交冲突而中断,更不用担心数据的备份.Github就是一个专门实现上述功能的开源平台。*

##  搭建git
------ 利用Chocolatey安装git


####  步骤
1. Chocolatey安装
2. 用Chocolatey安装git

####  详解

- Chocolatey安装

    - 以管理员打开PowerShell，输入命令<br/>
    ```
    Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
    ```

	- **或**：以管理员打开cmd，输入命令<br/>
    ```
    @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
    ```

    - 测试：在PowerShell或cmd，输入`choco`或`choco -?`

    - 注：升级Chocolatey的命令(在PowerShell或cmd中输入)：`choco upgrade chocolatey`


- 用Chocolatey安装git

    - 打开管理员权限PowerShell
	- 输入`choco install git -y`
	- 测试：能够打开git Bash


##  搭建Github
------ 利用git安装、配置、测试Github

####  步骤详解

- [Github官网](https://desktop.github.com/)下载桌面版，并安装。

- 注册一个Github账号：用户名，邮箱，密码

- 检查本机是否有ssh key设置<br/>

    打开git bash客户端：<br/>
    `$ cd ~/.ssh 或cd .ssh`
    <BR/>如果没有则提示： `No such file or directory`<BR/>
    如果有则进入~/.ssh路径下：<br/>
        `ls` 查看当前路径文件<br/>
        `rm *` 删除所有文件

- 使用Git Bash生成新的ssh key
    
    - 保证当前路径在”~”下`$ cd ~` 
    - 输入
        ```
        $ ssh-keygen -t rsa -C "xxxxxx@yy.com"  #建议填写自己真实有效的邮箱地址
        
        Generating public/private rsa key pair.
        Enter file in which to save the key (/c/Users/xxxx_000/.ssh/id_rsa):   #开始设置（ **直接回车** ）
        Enter passphrase (empty for no passphrase):   #输入密码（ **直接回车** ）
        Enter same passphrase again:   #再次确认密码（ **直接回车** ）
        Your identification has been saved in /c/Users/xxxx_000/.ssh/id_rsa.   #生成的id_rsa文件为密钥
        Your public key has been saved in /c/Users/xxxx_000/.ssh/id_rsa.pub.  #生成的id_rsa.pub公钥

        The key fingerprint is:
        e3:51:33:xx:xx:xx:xx:xxx:61:28:83:e2:81 xxxxxx@yy.com   
        ```

    - 本机已完成ssh key设置，其存放路径为：c:/Users/xxxx_000/.ssh/下，文件名称为id_rsa.pub。

- 添加ssh key到GitHub
    - 登录GitHub账号；
    - 点击右上角账号头像的“▼”→Settings→SSH kyes→Add SSH key。
    - 复制id_rsa.pub的公钥内容。
    - 进入c:/Users/xxxx_000/.ssh/目录下，用记事本打开id_rsa.pub文件，全选复制公钥内容。
    - Title自定义，将公钥粘贴到GitHub中Add an SSH key的key输入框，最后“Add Key”。

- 配置账户
    - 打开Git Bash，输入<br/>
    `$ git config --global user.name “your_username”  #设置用户名`<br/>
    `$ git config --global user.email “your_registered_github_Email”  #设置邮箱地址(建议用注册giuhub的邮箱)`

- 测试ssh keys是否设置成功<br/>

    `$ ssh -T git@github.com`<br/>
    ```
    The authenticity of host 'github.com (192.30.252.129)' can't be established.`
    RSA key fingerprint is 16:27:xx:xx:xx:xx:xx:4d:eb:df:a6:48.
    Are you sure you want to continue connecting (yes/no)? yes #确认你是否继续联系，输入yes
    Warning: Permanently added 'github.com,192.30.252.129' (RSA) to the list of known hosts.
    Enter passphrase for key '/c/Users/xxxx_000/.ssh/id_rsa':  #生成ssh kye是密码为空则无此项，若设置有密码则有此项且，输入生成ssh key时设置的密码即可。
    Hi xxx! You've successfully authenticated, but GitHub does not provide shell access. #出现词句话，说明设置成功。
    ```

- 登陆Github桌面版

- 新建Responds设置clone本地位置

- 测试：本地文件变化之后；通过Github桌面版先Submit，后Push到Github；打开网页版后查看是否有该仓库。

- 教程参考：
    - 教程1：https://www.jianshu.com/p/6ae3697a7c93
    - 教程2：https://www.liaoxuefeng.com/wiki/896043488029600
 