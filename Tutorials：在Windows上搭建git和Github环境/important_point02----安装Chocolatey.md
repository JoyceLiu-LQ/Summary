#  �ؼ�����

##  ����PowerShell����

```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

###  ����
1. Windows �İ���������Chocolatey - ��������Զ���,�ǻ��� PowerShell����Ҫ�����Զ��ӻ�����������ֿ�����������װ��������ж����������ϵͳ��
2. ����ִ�в��Ը�ʽ:  

    > Set-ExecutionPolicy  
    >   [-ExecutionPolicy] \<ExecutionPolicy\>  
    >   [ [-Scope] \<ExecutionPolicyScope\>]  
    >   [-Force][-WhatIf]  
    >   [-Confirm]  
    >   [\<CommonParameters\>]  

3. Set-ExecutionPolicy������ִ�в��ԡ�  
    - ר��ΪPowerShell��ƵĽű�ִ�в��ԣ���Ҫ���ڲ�ͬ��Ӧ�ó��������ò�ͬ�Ĳ�������ֹ����ű���ִ�С�
    - ��������ִ�в��Զ�Ҫ�ڹ���ԱȨ���µ�PowerShell����
    - �����ִ�Сд��
    - \<ExecutionPolicy\> �ṩ�� Restricted��AllSigned��RemoteSigned��Unrestricted��Bypass��Undefined �������͵�ִ�в���.
        - Restricted(�����Ƶ�):
            - ��ֹ�������нű��ļ���������ʽ���������ļ���.ps1xml����ģ��ű��ļ���.psm1����PowerShell�����ļ���.ps1����
            - ��Ĭ�ϵ�ִ�в���
            - ����취��  
                Ҫ����PowerShell�ű�������Ҫ�������ò��ԣ�  
                `Set-ExecutionPolicy Bypass`  
        - AllSigned(������ǩ����)��
            - ֻ����ִ�����о�������ǩ���Ľű�
            - ��������� PowerShell �ű���û������ǩ����
            - ����취��  
                [��һ�� PowerShell �ű�ǩ��(��������ǩ��)](https://www.cnblogs.com/sparkdev/p/7460518.html)��
        - RemoteSigned
            - ��ִ�д����������صĽű�ʱ����Ҫ�ű���������ǩ�������򲻻���������ű���  
                ������ڱ��ش����Ľű������ֱ��ִ�У���Ҫ��ű���������ǩ����  
        
        - Unrestricted
            - ��������δǩ���Ľű�
            - �����������صĽű���������ǰ����а�ȫ����ʾ
        - Bypass
            - �Խű���ִ�в����κε����ƣ��κνű�������ִ�У����Ҳ����а�ȫ����ʾ��
            - ��ִ�в��������ڽ�PowerShell�ű����õ��ϴ��Ӧ�ó����е����ã�����������PowerShell�Ǿ����Լ��İ�ȫģ�͵ĳ���Ļ��������á�
        - Undefined
            - û�����ýű�����
            - �ᷢ���̳л�Ӧ��Ĭ�ϵĽű�����
            
4. Scope ExecutionPolicy
    - ָ����ִ�в���Ӱ��ķ�Χ��Ĭ�Ϸ�Χ��LocalMachine��
        - MachinePolicy���������Ϊ������������û����á�
        - UserPolicy���ɼ������ǰ�û�����������á�
        - Process�����򡣽�Ӱ�쵱ǰ��PowerShell�Ự��
        - CurrentUser����Ӱ�쵱ǰ�û���
        - LocalMachine��Ӱ�����������û���Ĭ�Ϸ�Χ��
    - [-Scope]����ʡ�ԡ�
5. -Force
    - ��ֹ����ȷ����ʾ��        
                
6. ����Ļ�������Ϊ��  
    > `Set-ExecutionPolicy Bypass Process -Force`  
    > ����һ��ִ�в��ԣ����԰�װһ����ȫ�Ƚϸߵ�PowerShell�ű����ԣ���Χ��Ӱ�쵱ǰ��PowerShell�Ự���ҽ�ֹ����ȷ����ʾ��
    
7. ���ţ�  
    - \[\]����д�ɲ�д
    - \<\>����ʾ��ѡ    
    
8. PowerShell ��������  
    - PowerShell ʹ�á�ν�� - ���ʡ�����ϵͳ�� ÿ�� cmdlet ���ƶ���һ����׼ν�ʡ����ַ����ض�������ɡ�

9. ��PowerShell��д�����룬�м�����÷ֺ�";"������

10. ����ps1�ű��ķ���  
    - ����һ��  
    `powershell IEX (New-Object Net.WebClient).DownloadString('https://raxxxxx/xxx.ps1');`  
    - ��������  
    `set-ExecutionPolicy RemoteSigned Import-Module .\xxxxx.ps1 [����ģ��]`

11. iex ������ Invoke-Expression �ı���Alias��
    - ���ģ����ñ��ʽ�������Ϊֱ�����С����������Ӵ��뱾���Ϳ���ֱ�����д��룬�������Ľ����
    - �䷨��  
        `Invoke-Expression [-command] <string> [<CommonParameters>]`  
        - [-command]  string��һ����Ч��PowerShell���ʽ�������ַ�����������ַ����ı�������  
        - [ CommonParameters ] ��-Verbose��-Debug��-ErrorAction��-ErrorVariable��-WarningAction��-WarningVariable��-OutBuffer -OutVariable��
        - Invoke-Expression�������⣺
            - ��ʹ�����ȷ�����ñ�ø���
            - ��ʹά���ű�����
            - �������Ʒ��
            - Ҳ���������� - ������һ������ע�빥���Ľű�
        - �������������ĳ�����������·���а����ո���ô����Ҫ������������'��'�������help about_operators�����ҡ�call operator������
        - ʹ�õ��ߣ�����ĳЩ����������������ʱ�����½ű���Invoke-Expression��һ������ǿ�������õ����
        
12. New-Object ������PowerShell�е�cmdlet ���
    - New-Object���ģ��½�����
    - New-Object ����һ��.NET Framework��COM�����ʵ����
    - �﷨1������һ��.NET Frameworkʵ��
        ```
        New-Object
        [-TypeName] <String>
        [[-ArgumentList] <Object[]>]
        [-Property <IDictionary>]
        [<CommonParameters>]
        ```
    - �﷨2������һ��COM�����ʵ��
        ```
        New-Object
        [-ComObject] <String>
        [-Strict]   
        [-Property <IDictionary>]
        [<CommonParameters>]
        ```
    - New-Object Net.WebClient�Ǵ���һ��.NET Frameworkʵ����ȫд��New-Object System.Net.WebClient
    - ������
        - -ArgumentList��ָ��Ҫ���ݸ�.NET Framework��Ĺ��캯���Ĳ����б�ʹ�ö��ţ������ָ��б��е�Ԫ�ء�ArgumentList�ı�����Args��
        - -Property��ָ������ֵ�������¶���ķ����������ϣ�����м������Ի򷽷������ƣ�ֵ������ֵ�򷽷�������  
            New-Object������������ÿ������ֵ�������������ڹ�ϣ���г��ֵ�˳�����ÿ��������  
        - -TypeName��ָ��.NET Framework��ı�׼���ơ�
    - ���룺Null�������Object��
    - New-Objectͨ���������кͽű�������ʹ��.NET Framework������չ��Windows�ű����������п��õĹ��ܡ�    
    
13. cmdlet����
    - ������Ϊ��command-let��������Windows PowerShell������ʹ�õ������������ִ�е������ܡ�
    - ÿ��cmdlet����һ�������ļ�������ͨ������`Get-Help <cmdlet-Name> -Detailed`�����ʸ��ļ���
    - ���еĻ���cmdlet������  
    
        |    ����    |    С����   |  
        | ---------- | ----------  |
        | Get-Location | ��ȡ��ǰĿ¼|  
        | Set-Location | ���ĵ�ǰĿ¼|  
        | Copy-Item | �����ļ� |  
        | Remove-Item | ɾ���ļ���Ŀ¼ |  
        | Move-Item | �ƶ��ļ� |  
        | Rename-Item | �������ļ� |  
        | New-Item | ����һ���µĿ��ļ���Ŀ¼ |  
        
    - Windows PowerShell�������ٶ����������cmdlet������ԱҲ���Ա�д�Լ���cmdlet����������
    - [cmdlet�Ĺ�����ʽ](https://docs.microsoft.com/en-us/powershell/developer/cmdlet/windows-powershell-cmdlet-concepts)
    - �û���Ҫһ��ɷ��ֵĺ�Ԥ�ڵ�cmdlet���ơ�ʹ���ʵ��Ķ��ʣ��Ա��û����Կ�������cmdlet�Ĺ��ܲ����ɷ���ϵͳ�Ĺ��ܡ�  
        ���磬���������������ȡ�����ԡ�start����ͷ��ϵͳ�ϵ�����������б�get-command start-*��  
        ʹ��cmdlet�е����ʽ�cmdlet������cmdlet���ֿ��������ʱ�ʾ��������ִ�в�������Դ�����������ɶ��ʱ�ʾ��  
       
14. System.Net.WebClient ��

    - �ṩ��URI��ʶ����Դ**��������**�ʹ���**��������**�ĳ��÷�����
        > ͳһ��Դ��ʶ����Ӣ�Uniform Resource Identifier����д��URI���ڼ������������һ�����ڱ�ʶĳһ��������Դ���Ƶ��ַ�����   
        > ���ֱ�ʶ�����û��������У�һ��ָ��ά��������Դͨ���ض���Э����н���������  
        > URI���������ʽ��ͳһ��Դ��λ����URL��������ָ��Ϊ����ʽ����ַ��  
        > ���������÷���ͳһ��Դ���ƣ�URN������Ŀ����ͨ���ṩһ��;����  
        > �������ض������ֿռ���Դ�ı�ʶ���Բ�����ַ��  
    
    - Ĭ������£�.NET Framework֧���뿪ͷ��URI http:��https:��ftp:����file:�����ı�ʶ����
    - [���еķ�����ϸ���](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient?view=netframework-4.8)  

15. ������DownloadString()

    `DownloadString('https://chocolatey.org/install.ps1')`  

    - �÷�����System.Net.WebClient���е�һ������Դ�������ݣ��ַ������ķ�����   
    
    - ���������Դ����ΪString��Ҫ���ص���Դ����ָ��Ϊ����URI���ַ�����Uri��
    
    - ���巵�ص�ֵ����ҳ��ű��е�Դ���롣

16. **����һ��.NET Framework���еķ���**  

    `(New-Object System.Net.WebClient).DownloadString('http://xxxx')`   

    - ���壺�½�һ�����󣬴�Web�ͻ��˵����У�Ŀ���Ƿ��ͻ��������
        
    - ����ֱ��д��.����(��WebClient.DownloadString)��  
        �����½�һ������Ķ����������ӵ��������е������ص㣬��һ�������ĸ��壬����Ⱥ�塣
        
    - (New-Object System.Net.WebClient)���½�һ�����û�����Ķ���  
        д������PowerShell�У�New-Object <.NET Framework��>  
        ��C#�У����� ������ = new ����();
        
    - .DownloadString('http://xxxx')��Ϊ��������Ķ����������һ��������  
        д��������.����()
    
17. ps1�ļ�  
    
    - [PowerShell��д�ͽű�������ϸ�̳�](https://www.pstips.net/powershell-create-and-start-scripts.html)

    - �򵥱�д��
        - �ű����ݶ̣�
            ```
            PS E:> '"Hello,Powershell Script"' > MyScript.ps1
            PS E:> .\MyScript.ps1
            Hello,Powershell Script
            ```
        - �ű����У��ű��ļ�ͨ��@'  ��  '@�պ�������  
            ������д����˫���ţ�Powershell���������ı������н���  
            
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

            2012��4��27�� 8:15:10
            C:\Program Files\Common Files
            files count
            20           
            ```    
        - ֱ����Powershell����̨�д�Notepad
            ```
            PS E:> notepad.exe .\MyScript.ps1
            PS E:> notepad.exe
            ```
        - ��Ҫ���ִ�в��Ե�ֵ��
        - ִ��һ������һ��ִ��һ���ű�������ű������·�����߾���·��������*.ps1��չ�������԰ѽű���ִ����䱣��Ϊ����
            ```
            PS E:> Set-Alias Invok-MyScript .\MyScript.ps1
            PS E:> Invok-MyScript
            
            2012��4��28�� 0:24:22
            C:\Program Files\Common Files
            files count
            20
            ```
        



