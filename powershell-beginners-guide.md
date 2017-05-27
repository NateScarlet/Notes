[TOC]

[原文](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell/powershell-beginners-guide.md)


PowerShell入门指南
====

如果您是PowerShell的新用户，本文将向您介绍一些PowerShell的一些基本思路。

我们建议您打开一个PowerShell控制台/会话，并按照本文档中的说明进行输入，以最大限度地利用此练习。


启动PowerShell控制台/会话
---
首先，您需要按照[安装PowerShell指南](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell/README.md#installing-powershell)启动PowerShell会话。

## 熟悉PowerShell命令

在本节中，您将学习如何
- 创建文件，删除文件并更改文件目录
- 发现您目前使用的PowerShell版本
- 退出PowerShell会话
- 如果您需要帮助
- 查找PowerShell cmdlet的语法
- 和更多

如上所述，PowerShell命令设计为具有Verb-Noun结构，例如Get-Process，Set-Location，Clear-Host等。
我们来练习一些基本的PowerShell命令，也称为**cmdlets**。

请注意，在以下示例中，我们将使用PowerShell提示符号**PS />**显示在Linux上。
它在Windows上显示为**PS C：\\>**。

**1. Get-Process**：获取在本地计算机或远程计算机上运行的进程。

默认情况下，您将获得类似于以下内容的数据：

``` PowerShell
PS /> Get-Process

Handles   NPM(K)    PM(K)     WS(K)     CPU(s)     Id    ProcessName
-------  ------     -----     -----     ------     --    -----------
    -      -          -           1      0.012     12    bash
    -      -          -          21     20.220    449    powershell
    -      -          -          11     61.630   8620    code
    -      -          -          74    403.150   1209    firefox

…
```
只对在您的计算机上运行的Firefox进程感兴趣？

尝试这个：

```PowerShell
PS /> Get-Process -Name firefox

Handles   NPM(K)    PM(K)     WS(K)    CPU(s)     Id   ProcessName
-------  ------     -----     -----    ------     --   -----------
    -      -          -          74   403.150   1209   firefox
```
想要收到多个流程？

那只需指定进程名称并用逗号分隔。

```PowerShell
PS /> Get-Process -Name firefox, powershell
Handles   NPM(K)    PM(K)     WS(K)    CPU(s)     Id   ProcessName
-------  ------     -----     -----    ------     --   -----------
    -      -          -          74   403.150   1209   firefox
    -      -          -          21    20.220    449   powershell
```

**2. Clear-Host**: 清除主机程序中的显示。
```PowerShell
PS /> Get-Process
PS /> Clear-Host
```
键入太多只是为了清除屏幕？

以下是别名的帮助。

**3. Get-Alias**: 获取当前会话的别名。
```PowerShell
PS /> Get-Alias

CommandType     Name
-----------     ----
…

Alias           cd -> Set-Location
Alias           cls -> Clear-Host
Alias           copy -> Copy-Item
Alias           dir -> Get-ChildItem
Alias           gc -> Get-Content
Alias           gmo -> Get-Module
Alias           ri -> Remove-Item
Alias           type -> Get-Content
…
```
As you can see "cls" is an alias of Clear-Host.
Now try it:
```PowerShell
PS /> Get-Process
PS /> cls
```
**4. cd - Set-Location**: 将当前工作位置设置为指定位置。
```PowerShell
PS /> Set-Location /home
PS /home>
```
**5. dir - Get-ChildItem**: 获取一个或多个指定位置的项目和子项目。

```PowerShell
Get all files under the current directory:

PS /> Get-ChildItem

Get all files under the current directory as well as its subdirectories:
PS /> cd $home
PS /home/jen> dir -Recurse

List all files with "txt" file extension.

PS /> cd $home
PS /home/jen> dir –Path *.txt -Recurse
```

**6. New-Item**: 创建一个新项目。

```PowerShell
An empty file is created if you type the following:
PS /home/jen> New-Item -Path ./test.txt


    Directory: /home/jen


Mode                LastWriteTime         Length  Name
----                -------------         ------  ----
-a----         7/7/2016   7:17 PM              0  test.txt
```
您可以使用**- Value**参数将一些数据添加到文件中。
例如，以下命令添加短语“Hello world!” 作为文件内容到test.txt。
因为test.txt文件已经存在，我们使用**- Force**参数替换现有的内容。

```PowerShell
PS /home/jen> New-Item -Path ./test.txt -Value "Hello world!" -Force

    Directory: /home/jen


Mode                LastWriteTime         Length  Name
----                -------------         ------  ----
-a----         7/7/2016   7:19 PM             24  test.txt
```
还有其他方法可以向文件添加一些数据。

例如，您可以使用Set-Content设置文件内容：

```PowerShell
PS /home/jen>Set-Content -Path ./test.txt -Value "Hello world again!"
```
或者简单地使用“>”如下：
```
# create an empty file
"" > test.txt  

# set "Hello world!" as content of test.txt file
"Hello world!!!" > test.txt
```
以上的井号（＃）用于PowerShell中的注释。

**7. type - Get-Content**: 获取指定位置的项目的内容。

```PowerShell
PS /home/jen> Get-Content -Path ./test.txt
PS /home/jen> type -Path ./test.txt

Hello world again!
```
**8. del - Remove-Item**: 删除指定的项目。

此cmdlet将删除/home/jen/test.txt文件:
```PowerShell
PS /home/jen> Remove-Item ./test.txt
```

**9. $PSVersionTable**: 显示当前正在使用的PowerShell的版本。

在PowerShell会话中键入**$PSVersionTable**，您将看到如下所示的内容。
“PSVersion”表示您正在使用的PowerShell版本。

```PowerShell
Name                           Value
----                           -----
PSVersion                      6.0.0-alpha
PSEdition                      Core
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   3.0.0.0
GitCommitId                    v6.0.0-alpha.12
CLRVersion                     
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1

```

**10. Exit**: 要退出PowerShell会话，请键入“exit”。
```PowerShell
PS /home/jen> exit
```


需要帮助？
----
PowerShell中最重要的命令可能是Get-Help，它允许您快速学习PowerShell，而无需在互联网上搜索。

Get-Help cmdlet还显示了PowerShell命令如何使用示例。

它显示了Get-Process cmdlet的语法和其他技术信息。

```PowerShell
PS /> Get-Help -Name Get-Process
```

它显示了如何使用Get-Process cmdlet的示例。
```PowerShell
PS />Get-Help -Name Get-Process -Examples
```

如果您使用**- Full**参数，例如“Get-Help -Name Get-Process -Full”，它将显示更多的技术信息。


发现系统上可用的命令
----

您想要发现系统上可用的PowerShell cmdlet？ 只需运行“Get-Command”，如下所示：
```PowerShell
PS /> Get-Command
```
如果您想知道系统上是否存在特定的cmdlet，可以执行以下操作：
```PowerShell
PS /> Get-Command Get-Process
```
如果您想知道Get-Process cmdlet的语法，请键入：
```PowerShell
PS /> Get-Command Get-Process -Syntax
```
如果您想知道如何使用Get-Process，请键入：
```PowerShell
PS /> Get-Help Get-Process -Example
```


PowerShell管道'|'
----
有时，当您运行Get-ChildItem或“dir”时，您希望以降序获取文件和文件夹列表。

要实现这一点，请键入：

```PowerShell
PS /home/jen> dir | Sort-Object -Descending
```
假设你想获得目录中最大的文件
```PowerShell
PS /home/jen> dir | Sort-Object -Property Length -Descending | Select-Object -First 1


    Directory: /home/jen


Mode                LastWriteTime       Length  Name
----                -------------       ------  ----
-a----        5/16/2016   1:15 PM        32972  test.log

```


如何创建和运行PowerShell脚本
----
您可以使用Visual Studio代码或您喜爱的编辑器来创建PowerShell脚本，并使用.ps1文件扩展名保存。

有关更多详细信息，请参阅 [创建和运行PowerShell脚本指南][https://raw.githubusercontent.com/PowerShell/PowerShell/master/docs/learning-powershell/create-powershell-scripts.md]


推荐培训阅读
----
-	Video: [Get Started with PowerShell][remoting] from Channel9
   -[eBooks from PowerShell.org](https://powershell.org/ebooks/)
   -[eBooks from PowerShell.com][ebooks-powershell.com]
    -[eBooks List][ebook-list] by Martin Schvartzman
    -[Tutorial from MVP][tutorial]
   -Script Guy blog: [The best way to Learn PowerShell][to-learn]
   -[Understanding PowerShell Module][ps-module]
   -[How and When to Create PowerShell Module][create-ps-module] by Adam Bertram
    -Video: [PowerShell Remoting in Depth][in-depth] from Channel9
   -[PowerShell Basics: Remote Management][remote-mgmt] from ITPro
    -[Running Remote Commands][remote-commands] from PowerShell Web Docs
    -[Samples for PowerShell Scripts][examples]
    -[Samples for Writing a PowerShell Script Module][examples-ps-module]
    -[Writing a PowerShell module in C#][writing-ps-module]
    -[Examples of Cmdlets Code][sample-code]



商业资源
----
- [Windows PowerShell in Action][in-action] by Bruce Payette
- [Windows PowerShell Cookbook][cookbook] by Lee Holmes

[in-action]: https://www.amazon.com/Windows-PowerShell-Action-Second-Payette/dp/1935182137
[cookbook]: http://shop.oreilly.com/product/9780596801519.do
[ebook-list]: https://blogs.technet.microsoft.com/pstips/2014/05/26/free-powershell-ebooks/
[ebooks-powershell.com]: http://powershell.com/cs/blogs/ebookv2/default.aspx
[tutorial]: http://www.computerperformance.co.uk/powershell/index.htm
[to-learn]:https://blogs.technet.microsoft.com/heyscriptingguy/2015/01/04/weekend-scripter-the-best-ways-to-learn-powershell/
[ps-module]:https://msdn.microsoft.com/en-us/library/dd878324%28v=vs.85%29.aspx
[create-ps-module]:http://www.tomsitpro.com/articles/powershell-modules,2-846.html
[remoting]:https://channel9.msdn.com/Series/GetStartedPowerShell3/06
[in-depth]: https://channel9.msdn.com/events/MMS/2012/SV-B406
[remote-mgmt]:http://windowsitpro.com/powershell/powershell-basics-remote-management
[remote-commands]:https://msdn.microsoft.com/en-us/powershell/scripting/core-powershell/running-remote-commands
[examples]:http://examples.oreilly.com/9780596528492/
[examples-ps-module]:https://msdn.microsoft.com/en-us/library/dd878340%28v=vs.85%29.aspx
[writing-ps-module]:http://www.powershellmagazine.com/2014/03/18/writing-a-powershell-module-in-c-part-1-the-basics/
[sample-code]:https://msdn.microsoft.com/en-us/library/ff602031%28v=vs.85%29.aspx
[create-run-script]:./create-powershell-scripts.md
