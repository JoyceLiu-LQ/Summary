# 关键步骤

##  输入PowerShell命令

```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

###  解释
1. Windows 的包管理器：Chocolatey - 软件管理自动化,是基于 PowerShell，主要用于自动从互联网的软件仓库中搜索、安装、升级、卸载软件或操作系统。
2. 设置执行策略格式:  

    > Set-ExecutionPolicy  
    >   [-ExecutionPolicy] \<ExecutionPolicy\>  
    >   [ [-Scope] \<ExecutionPolicyScope\>]  
    >   [-Force][-WhatIf]  
    >   [-Confirm]  
    >   [\<CommonParameters\>]  

3. Set-ExecutionPolicy：设置执行策略。  
    - 专门为PowerShell设计的脚本执行策略，主要是在不同的应用场景中设置不同的策略来防止恶意脚本的执行。
    - 所有设置执行策略都要在管理员权限下的PowerShell运行
    - 不区分大小写。
    - \<ExecutionPolicy\> 提供了 Restricted、AllSigned、RemoteSigned、Unrestricted、Bypass、Undefined 六种类型的执行策略.
        - Restricted(受限制的):
            - 阻止运行所有脚本文件，包括格式化和配置文件（.ps1xml），模块脚本文件（.psm1）和PowerShell配置文件（.ps1）。
            - 是默认的执行策略
            - 解决办法：  
                要运行PowerShell脚本，首先要调整设置策略：  
                `Set-ExecutionPolicy Bypass`  
        - AllSigned(有数字签名的)：
            - 只允许执行所有具有数字签名的脚本
            - 绝大多数的 PowerShell 脚本是没有数字签名的
            - 解决办法：  
                [给一个 PowerShell 脚本签名(打上数字签名)](https://www.cnblogs.com/sparkdev/p/7460518.html)：
        - RemoteSigned
            - 当执行从网络上下载的脚本时，需要脚本具有数字签名，否则不会运行这个脚本。  
                如果是在本地创建的脚本则可以直接执行，不要求脚本具有数字签名。  
        
        - Unrestricted
            - 允许运行未签名的脚本
            - 从网络上下载的脚本，在运行前会进行安全性提示
        - Bypass
            - 对脚本的执行不设任何的限制，任何脚本都可以执行，并且不会有安全性提示。
            - 此执行策略适用于将PowerShell脚本内置到较大的应用程序中的配置，或者适用于PowerShell是具有自己的安全模型的程序的基础的配置。
        - Undefined
            - 没有设置脚本策略
            - 会发生继承或应用默认的脚本策略
            
4. Scope ExecutionPolicy
    - 指定受执行策略影响的范围。默认范围是LocalMachine。
        - MachinePolicy：由组策略为计算机的所有用户设置。
        - UserPolicy：由计算机当前用户的组策略设置。
        - Process：仅影响当前的PowerShell会话。
        - CurrentUser：仅影响当前用户。
        - LocalMachine：影响计算机所有用户的默认范围。
    - [-Scope]可以省略。
5. Force
    - 禁止所有确认提示。        
                
6. 命令的基本意义为：  
    > `Set-ExecutionPolicy Bypass Process`  
    > 设置一个执行策略，可以安装一个安全度较高的PowerShell脚本语言，范围仅影响当前的PowerShell会话。
    
7. 符号：  
    - \[\]：可写可不写
    - \<\>：表示必选    
    
8. PowerShell 的命名：  
    - PowerShell 使用“谓词 - 名词”命名系统。 每个 cmdlet 名称都由一个标准谓词、连字符和特定名词组成。

9. 在PowerShell中写多句代码，中间可以用分号";"隔开。

10. 加载ps1脚本  
    - 方法一：  
    `powershell IEX (New-Object Net.WebClient).DownloadString('https://raxxxxx/xxx.ps1');`  
    - 方法二：  
    `set-ExecutionPolicy RemoteSigned Import-Module .\xxxxx.ps1 [导入模块]`

11. iex 命令是 Invoke-Expression 的别名Alias。
    - 中文：调用表达式
    - 句法：  
        `Invoke-Expression [-command] <string> [<CommonParameters>]`  
        - [-command]  string：一个有效的PowerShell表达式的文字字符串（或包含字符串的变量）。  
        - [ CommonParameters ] ：-Verbose，-Debug，-ErrorAction，-ErrorVariable，-WarningAction，-WarningVariable，-OutBuffer -OutVariable。
        - Invoke-Expression存在问题：
            - 它使获得正确的引用变得复杂
            - 它使维护脚本更难
            - 它比替代品慢
            - 也许最糟糕的是 - 它打开了一个代码注入攻击的脚本
        - 如果您正在运行某个命令并且命令路径中包含空格，那么您需要命令调用运算符'＆'（请参阅help about_operators，查找“call operator”）。
        - 使用底线：对于某些场景，例如在运行时创建新脚本，Invoke-Expression是一个功能强大且有用的命令。
        
12. New-Object 命令是PowerShell中的cmdlet 命令。
    - New-Object中文：新建对象
    - New-Object 创建一个.NET Framework或COM对象的实例。
    - 语法1：创建一个.NET Framework实例
        ```
        New-Object
        [-TypeName] <String>
        [[-ArgumentList] <Object[]>]
        [-Property <IDictionary>]
        [<CommonParameters>]
        ```
    - 语法2：创建一个COM对象的实例
        ```
        New-Object
        [-ComObject] <String>
        [-Strict]   
        [-Property <IDictionary>]
        [<CommonParameters>]
        ```
    - New-Object Net.WebClient是创建一个.NET Framework实例，全写是New-Object System.Net.WebClient
    - 
    
13. cmdlet命令
    - （发音为“command-let”），是Windows PowerShell环境中使用的轻量级命令。它执行单个功能。
    - 
    