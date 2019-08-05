#  关键步骤

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
        - Process：程序。仅影响当前的PowerShell会话。
        - CurrentUser：仅影响当前用户。
        - LocalMachine：影响计算机所有用户的默认范围。
    - [-Scope]可以省略。
5. -Force
    - 禁止所有确认提示。        
                
6. 命令的基本意义为：  
    > `Set-ExecutionPolicy Bypass Process -Force`  
    > 设置一个执行策略，可以安装一个安全度较高的PowerShell脚本语言，范围仅影响当前的PowerShell会话，且禁止所有确认提示。
    
7. 符号：  
    - \[\]：可写可不写
    - \<\>：表示必选    
    
8. PowerShell 的命名：  
    - PowerShell 使用“谓词 - 名词”命名系统。 每个 cmdlet 名称都由一个标准谓词、连字符和特定名词组成。

9. 在PowerShell中写多句代码，中间可以用分号";"隔开。

10. 加载ps1脚本的方法  
    - 方法一：  
    `powershell IEX (New-Object Net.WebClient).DownloadString('https://raxxxxx/xxx.ps1');`  
    - 方法二：  
    `set-ExecutionPolicy RemoteSigned Import-Module .\xxxxx.ps1 [导入模块]`

11. iex 命令是 Invoke-Expression 的别名Alias。
    - 中文：调用表达式。可理解为直接运行。（如果后面加代码本身，就可以直接运行代码，输出代码的结果）
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
    - 参数：
        - -ArgumentList：指定要传递给.NET Framework类的构造函数的参数列表。使用逗号（，）分隔列表中的元素。ArgumentList的别名是Args。
        - -Property：指定属性值并调用新对象的方法。输入哈希表，其中键是属性或方法的名称，值是属性值或方法参数。  
            New-Object创建对象并设置每个属性值，并按照它们在哈希表中出现的顺序调用每个方法。  
        - -TypeName：指定.NET Framework类的标准名称。
    - 输入：Null；输出：Object。
    - New-Object通过从命令行和脚本中轻松使用.NET Framework对象，扩展了Windows脚本宿主环境中可用的功能。    
    
13. cmdlet命令
    - （发音为“command-let”），是Windows PowerShell环境中使用的轻量级命令。它执行单个功能。
    - 每个cmdlet都有一个帮助文件，可以通过键入`Get-Help <cmdlet-Name> -Detailed`来访问该文件。
    - 流行的基本cmdlet包括：  
    
        |    功能    |    小命令   |  
        | ---------- | ----------  |
        | Get-Location | 获取当前目录|  
        | Set-Location | 更改当前目录|  
        | Copy-Item | 复制文件 |  
        | Remove-Item | 删除文件或目录 |  
        | Move-Item | 移动文件 |  
        | Rename-Item | 重命名文件 |  
        | New-Item | 创建一个新的空文件或目录 |  
        
    - Windows PowerShell包含两百多个基本核心cmdlet，管理员也可以编写自己的cmdlet并共享它们
    - [cmdlet的工作方式](https://docs.microsoft.com/en-us/powershell/developer/cmdlet/windows-powershell-cmdlet-concepts)
    - 用户需要一组可发现的和预期的cmdlet名称。使用适当的动词，以便用户可以快速评估cmdlet的功能并轻松发现系统的功能。  
        例如，以下命令行命令获取名称以“start”开头的系统上的所有命令的列表：get-command start-*。  
        使用cmdlet中的名词将cmdlet与其他cmdlet区分开来。名词表示将在其上执行操作的资源。操作本身由动词表示。  
       
14. System.Net.WebClient 类

    - 提供向URI标识的资源**发送数据**和从其**接收数据**的常用方法。
        > 统一资源标识符（英语：Uniform Resource Identifier，缩写：URI）在计算机术语中是一个用于标识某一互联网资源名称的字符串。   
        > 该种标识允许用户对网络中（一般指万维网）的资源通过特定的协议进行交互操作。  
        > URI的最常见的形式是统一资源定位符（URL），经常指定为非正式的网址。  
        > 更罕见的用法是统一资源名称（URN），其目的是通过提供一种途径。  
        > 用于在特定的名字空间资源的标识，以补充网址。  
    
    - 默认情况下，.NET Framework支持与开头的URI http:，https:，ftp:，和file:方案的标识符。
    - [类中的方法详细情况](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient?view=netframework-4.8)  

15. 方法：DownloadString()

    `DownloadString('https://chocolatey.org/install.ps1')`  

    - 该方法是System.Net.WebClient类中的一个从资源下载数据（字符串）的方法。   
    
    - 将请求的资源下载为String。要下载的资源可以指定为包含URI的字符串或Uri。
    
    - 具体返回的值是网页或脚本中的源代码。

16. **调用一个.NET Framework类中的方法**  

    `(New-Object System.Net.WebClient).DownloadString('http://xxxx')`   

    - 意义：新建一个对象，从Web客户端的类中，目的是发送或接收数据
        
    - 不能直接写类.方法(像WebClient.DownloadString)。  
        必须新建一个具体的对象，这个对象拥有这个类中的所有特点，是一个单独的个体，不是群体。
        
    - (New-Object System.Net.WebClient)是新建一个类的没命名的对象。  
        写法：在PowerShell中，New-Object <.NET Framework类>  
        在C#中，类名 对象名 = new 类名();
        
    - .DownloadString('http://xxxx')是为这个无名的对象调用类中一个方法。  
        写法：对象.方法()
    
17. ps1文件  
    
    - [PowerShell编写和脚本运行详细教程](https://www.pstips.net/powershell-create-and-start-scripts.html)

    - 简单编写：
        - 脚本内容短：
            ```
            PS E:> '"Hello,Powershell Script"' > MyScript.ps1
            PS E:> .\MyScript.ps1
            Hello,Powershell Script
            ```
        - 脚本多行：脚本文件通过@'  和  '@闭合起来；  
            单引号写成了双引号，Powershell将会把里面的变量进行解析  
            
           ```
            PS E:> @'
            >> Get-Date
            >> $Env:CommonProgramFiles
            >> #Script End
            >> "files count"
            >> (ls).Count
            >> #Script Really End
            >> '@ > myscript.ps1
            >>
            PS E:> .\MyScript.ps1

            2012年4月27日 8:15:10
            C:\Program Files\Common Files
            files count
            20           
            ```    
        - 直接在Powershell控制台中打开Notepad
            ```
            PS E:> notepad.exe .\MyScript.ps1
            PS E:> notepad.exe
            ```
        - 需要变更执行策略的值。
        - 执行一个命令一样执行一个脚本，输入脚本的相对路径或者绝对路径，包括*.ps1扩展名，可以把脚本的执行语句保存为别名
            ```
            PS E:> Set-Alias Invok-MyScript .\MyScript.ps1
            PS E:> Invok-MyScript
            
            2012年4月28日 0:24:22
            C:\Program Files\Common Files
            files count
            20
            ```
        



