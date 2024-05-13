---
title: 渗透测试入门之入DC1
date: 2024-05-13 20:42:32
tags: 网络安全
---



# 主机发现

ifconfig找到网段

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513102005699.png" alt="image-20240513102005699" style="zoom:67%;" />

kali主机ip.80

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513101825846.png" alt="image-20240513101825846" style="zoom:50%;" />

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513101913752.png" alt="image-20240513101913752" style="zoom:67%;" />

主机ip是.45

也就是说最后

测试每一个url访问主机。

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513102244190.png" alt="image-20240513102244190" style="zoom: 50%;" />

# 端口扫描

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513102628958.png" alt="image-20240513102628958" style="zoom:50%;" />

扫描获得开放的tcp以及udp端口

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513102859656.png" alt="image-20240513102859656" style="zoom:67%;" />

看起来udp并没有开放服务？或者受到防火墙阻拦

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513103102596.png" alt="image-20240513103102596" style="zoom:67%;" />

大多是port unreachable

# 发现漏洞

![image-20240513112859739](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513112859739.png)

通过msf漏洞数据库发现漏洞

![image-20240513113724368](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513113724368.png)

发现有大量的漏洞可以供使用。

信息：

> ### 漏洞详情：
>
> - **模块名称**：`exploit/unix/webapp/drupal_coder_exec`
> - **披露日期**：2016-07-13
> - **评级**：Excellent
> - **利用条件**：Yes
> - **漏洞描述**：Drupal Coder模块在处理用户输入时存在不当的输入验证，这使得远程攻击者可以通过发送精心构造的请求到目标服务器来利用这个漏洞。成功利用此漏洞可能允许攻击者在处理上下文中执行任意代码。

> ### 漏洞详情：
>
> - **模块名称**：`exploit/unix/webapp/drupal_drupalgeddon2`
> - **披露日期**：2018-03-28
> - **评级**：Excellent
> - **利用条件**：Yes
> - **漏洞描述**：Drupal的Forms API中存在一处远程代码执行漏洞。Drupal的Forms API在处理AJAX请求时，没有对用户输入进行充分的验证和清理，这使得攻击者可以通过发送恶意构造的AJAX请求来利用这个漏洞。成功利用此漏洞可能允许攻击者在处理上下文中执行任意代码。
>
> ### 影响范围：
>
> - **受影响版本**：Drupal 6.x，7.x，8.x
> - **影响组件**：Drupal的Forms API。
>
> ### 漏洞利用：
>
> 攻击者可以通过以下步骤利用此漏洞：
>
> 1. 1.**发送恶意请求**：攻击者构造特定的AJAX请求，这些请求包含恶意代码或命令。
>
> 2. 2.**执行代码**：当Drupal的Forms API处理这些请求时，它会执行其中的代码，从而允许攻击者执行任意命令。
>
> 3. 3.**控制服务器**：攻击者可以利用执行的命令来获取服务器的控制权，包括但不限于上传文件、修改文件、执行系统命令等。

> ### 漏洞详情：
>
> - **模块名称**：`exploit/multi/http/drupal_drupageddon`
> - **披露日期**：2014-10-15
> - **评级**：Excellent
> - **利用条件**：No
> - **漏洞描述**：Drupal的HTTP参数处理中存在SQL注入漏洞。当Drupal处理HTTP请求中的键值对时，没有对用户输入进行充分的验证和清理，这使得攻击者可以通过发送恶意构造的请求来利用这个漏洞。成功利用此漏洞可能允许攻击者在处理上下文中执行任意代码。

> ### 漏洞详情：
>
> - **模块名称**：`auxiliary/gather/drupal_openid_xxe`
> - **披露日期**：2012-10-17
> - **评级**：Normal
> - **利用条件**：Yes
> - **漏洞描述**：Drupal OpenID模块在处理XML数据时存在外部实体注入漏洞。当Drupal OpenID模块处理包含外部实体的XML数据时，没有进行适当的验证和清理，这使得攻击者可以通过发送恶意构造的XML请求来利用这个漏洞。成功利用此漏洞可能允许攻击者泄露敏感信息或执行其他攻击。

> `exploit/unix/webapp/drupal_restws_exec` 是一个Metasploit框架中的漏洞利用模块，它针对的是Drupal RESTWS模块的一个远程PHP代码执行漏洞。这个漏洞允许攻击者在没有身份验证的情况下执行任意PHP代码，从而完全控制受影响的Drupal网站。
>
> ### 漏洞详情：
>
> - **模块名称**：`exploit/unix/webapp/drupal_restws_exec`
> - **披露日期**：2016-07-13
> - **评级**：Excellent
> - **利用条件**：Yes
> - **漏洞描述**：Drupal RESTWS模块在处理RESTful Web Services请求时存在不当的输入验证，这使得远程攻击者可以通过发送精心构造的请求到目标服务器来利用这个漏洞。成功利用此漏洞可能允许攻击者在处理上下文中执行任意PHP代码。

# 漏洞攻击

采用第一个漏洞进行攻击

![image-20240513115507078](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513115507078.png)

设置攻击主机

![image-20240513115558111](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513115558111.png)没有获取到相关信息

采用另一个漏洞进行攻击

![image-20240513115943704](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513115943704.png)

已经成功地在目标主机上建立了一个Meterpreter会话，这意味着现在可以远程控制该主机

![image-20240513120204902](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513120204902.png)

ls查看当前目录文件

里面有一个flag1.txt

![image-20240513120420577](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513120420577.png)

找到其中的flag文件

看来是需要找到config文件

百度发现默认配置文件

![image-20240513120802723](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513120802723.png)

![image-20240513121653327](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513121653327.png)

在内部可以看到采用mysql数据库，用户名以及密码也得知了。

查阅之后发现

> 1. 1.**加载MySQL扩展**：
>    在Meterpreter会话中，首先需要加载MySQL扩展。您可以使用以下命令来加载它：`load mysql `
>
> 2. 2.**连接到MySQL服务器**：
>    加载扩展后，您可以使用以下命令来连接到MySQL服务器：`mysql_connect -h <host> -u <username> -p `将 `<host>` 替换为MySQL服务器的主机名或IP地址，将 `<username>` 替换为您的MySQL用户名。系统会提示您输入密码，输入后按回车键。
>
> 3. 3.**执行MySQL命令**：
>    连接成功后，您可以使用 `mysql_query` 命令来执行SQL命令。例如，要列出所有数据库，您可以使用：`mysql_query "SHOW DATABASES;" `
>
> 4. 4.**断开连接**：
>    完成操作后，您可以使用以下命令来断开与MySQL服务器的连接：`mysql_close`

![image-20240513162712176](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513162712176.png)

直接访问shell命令被拒绝了。

可以使用Hydra进行暴力破解

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513163803205.png" alt="image-20240513163803205" style="zoom: 50%;" />

与我的系统进行比较

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513164056151.png" alt="image-20240513164056151" style="zoom:67%;" />

在其中发现了一个flag4的用户。

采用hydra破解，字典会放在kali中的目录，有很多可以选择。

> 1. **
>    /usr/share/wordlists/**：这是默认的字典文件存放目录，包含各种类型的字典，用于密码爆破、漏洞扫描等。
>
> 2. 2.**/usr/share/seclists/**：来自SecLists项目的多个字典文件，涵盖密码、用户名、敏感文件路径、漏洞利用等方面的内容。
>
> 3. 3.**/usr/share/dirb/**：DirBuster工具的字典文件目录，用于穷举目录和文件路径。
>
> 4. 4.**/usr/share/john/**：John the Ripper工具的字典文件目录，用于密码破解。
>
> 5. 5.**/usr/share/sqlmap/**：SQLMap工具的字典文件目录，用于自动化SQL注入检测。
>
> 6. 6.**/usr/share/metasploit-framework/data/wordlists/**：Metasploit框架中的字典文件，适用于不同类型的渗透测试活动。
>
> 7. 7.**/usr/share/nmap/nselib/data/**：Nmap工具的字典文件目录，包含用于脚本和扫描的字典。
>
> 8. 8.**/usr/share/wfuzz/wordlist/**：wfuzz工具的字典文件目录，用于Web应用程序渗透测试。
>
> 9. 9.**/usr/share/wordlists/wfuzz/**：另一个用于wfuzz的字典文件目录。
>
> 10. 10.**/usr/share/wordlists/rockyou.txt.gz**：RockYou字典文件，这是一个广泛使用的密码字典。
>
> 11. 11.**/usr/share/crunch/**：Crunch工具的字典文件目录，用于生成自定义密码字典。
>
> 12. 12.**/usr/share/wordlists/fasttrack.txt**：Fast-Track字典文件，用于渗透测试活动。
>
> 13. 13.**/usr/share/wordlists/davinci.txt**：DaVinci字典文件，也是用于渗透测试。

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513164900444.png" alt="image-20240513164900444" style="zoom:67%;" />

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513164912515.png" alt="image-20240513164912515" style="zoom:67%;" />

可以看到此时已经获得了密码orange

但是回到靶机发现很多命令不能执行，在shell中也是一样。

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513165845777.png" alt="image-20240513165845777" style="zoom:67%;" />

查阅后发现提供了execute供使用。

> 1. **执行单个命令**：
>
> ```
> execute -f <command>
> ```
>
> 这个用法允许你在目标系统上执行一个单独的命令。例如：
>
> ```
> execute -f whoami
> ```
>
> 这将在目标系统上执行`whoami`命令，并显示当前用户的用户名。
>
> 1. **执行命令并返回结果**：
>
> ```
> execute -f <command> -i
> ```
>
> 这个用法与第一个相似，但它会在Meterpreter会话中返回命令的输出。例如：
>
> ```
> execute -f netstat -an -i
> ```
>
> 这将在目标系统上执行`netstat -an`命令，并将结果返回给Meterpreter会话。
>
> 1. **以交互式方式执行命令**：
>
> ```
> execute -f <command> -i -H
> ```
>
> 这个用法允许你在目标系统上以交互式方式执行命令。这对于需要用户输入的命令非常有用。例如：
>
> ```
> execute -f /bin/bash -i -H
> ```
>
> 这将在目标系统上启动一个交互式bash shell，并将控制权返回给Meterpreter，允许你在目标系统上执行更多的命令。
>
> 1. **以特定用户身份执行命令**：
>
> ```
> execute -f <command> -u <username>
> ```
>
> 这个用法允许你以指定用户的身份执行命令。例如：
>
> ```
> execute -f /bin/ls -u john
> ```
>
> 这将以`john`用户的身份在目标系统上执行`ls`命令。

`execute -f`用于执行外部程序或脚本文件，而直接输入命令用于执行目标系统上已存在的可执行文件。

通过ssh连接靶机

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513171613557.png" alt="image-20240513171613557" style="zoom:67%;" />

目前已经成功作为用户登录进入。

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513171656922.png" alt="image-20240513171656922" style="zoom:67%;" />

获取到相应信息。

<img src="E:/hexo/1PHAN-7878.github.io/source/images/image-20240513172048521.png" alt="image-20240513172048521" style="zoom:67%;" />

通过数据库密码登录进入。

![image-20240513172153220](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513172153220.png)

进入数据库，查看有哪些表。

![image-20240513172254191](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513172254191.png)

找到users表，存放的应该是管理员等的信息。但是密码应该加入了hash，看看能不能进行编码或者解码。

通过find命令可以找到password-hash.sh运行时出现了问题

![image-20240513184725095](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513184725095.png)

在通过find去找password.inc

![image-20240513184827197](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513184827197.png)

此时可以得到一个123456的hash值，作为我即将更改的密码。

![image-20240513190841804](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513190841804.png)

对数据库进行更改。

![image-20240513191006800](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513191006800.png)

用刚刚修改的管理员账号密码登录

![image-20240513191134069](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513191134069.png)

找到falg3

![image-20240513191208737](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513191208737.png)

# 提权

`find / -perm /4000`命令用于查找具有SUID（Set User ID）权限的文件。SUID权限允许普通用户在执行特定可执行文件时以文件所有者的身份运行，这可能包括root权限。

find -name flag4.txt -exec /bin/bash -p \;

当`find`命令找到一个名为`flag4.txt`的文件时，它会在该文件上执行`/bin/bash -p`命令，从而打开一个新的Bash shell，并尝试以特权模式运行。

![image-20240513193838583](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513193838583.png)

![image-20240513193936989](E:/hexo/1PHAN-7878.github.io/source/images/image-20240513193936989.png)

最终在/root文件夹下找到finalflag。

