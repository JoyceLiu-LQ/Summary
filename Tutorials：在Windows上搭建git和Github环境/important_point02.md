# �ؼ�����

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
        - Process����Ӱ�쵱ǰ��PowerShell�Ự��
        - CurrentUser����Ӱ�쵱ǰ�û���
        - LocalMachine��Ӱ�����������û���Ĭ�Ϸ�Χ��
    - [-Scope]����ʡ�ԡ�
5. Force
    - ��ֹ����ȷ����ʾ��        
                
6. ����Ļ�������Ϊ��  
    > `Set-ExecutionPolicy Bypass Process`  
    > ����һ��ִ�в��ԣ����԰�װһ����ȫ�Ƚϸߵ�PowerShell�ű����ԣ���Χ��Ӱ�쵱ǰ��PowerShell�Ự��
    
7. ���ţ�  
    - \[\]����д�ɲ�д
    - \<\>����ʾ��ѡ    
    
8. PowerShell ��������  
    - PowerShell ʹ�á�ν�� - ���ʡ�����ϵͳ�� ÿ�� cmdlet ���ƶ���һ����׼ν�ʡ����ַ����ض�������ɡ�

9. ��PowerShell��д�����룬�м�����÷ֺ�";"������

10. ����ps1�ű�  
    - ����һ��  
    `powershell IEX (New-Object Net.WebClient).DownloadString('https://raxxxxx/xxx.ps1');`  
    - ��������  
    `set-ExecutionPolicy RemoteSigned Import-Module .\xxxxx.ps1 [����ģ��]`

11. iex ������ Invoke-Expression �ı���Alias��
    - ���ģ����ñ��ʽ
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
    - 
    
13. cmdlet����
    - ������Ϊ��command-let��������Windows PowerShell������ʹ�õ������������ִ�е������ܡ�
    - 
    