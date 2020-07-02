## Linux 系统中的目录

![](https://raw.githubusercontent.com/geekzsp/ImagesRepository/master/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f332f313634356631633635363736636166363f773d38323326683d33313526663d706e6726733d3135323236.png)

| 目录           | 评论                                                         |
| :------------- | :----------------------------------------------------------- |
| /              | 根目录，万物起源。                                           |
| /bin           | 包含系统启动和运行所必须的二进制程序。                       |
| /boot          | 包含 Linux 内核、初始 RAM 磁盘映像（用于启动时所需的驱动）和 启动加载程序。有趣的文件：/boot/grub/grub.conf or menu.lst， 被用来配置启动加载程序。/boot/vmlinuz，Linux 内核。 |
| /dev           | 这是一个包含设备结点的特殊目录。“一切都是文件”，也适用于设备。 在这个目录里，内核维护着所有设备的列表。 |
| /etc           | 这个目录包含所有系统层面的配置文件。它也包含一系列的 shell 脚本， 在系统启动时，这些脚本会开启每个系统服务。这个目录中的任何文件应该是可读的文本文件。有趣的文件：虽然/etc 目录中的任何文件都有趣，但这里只列出了一些我一直喜欢的文件：/etc/crontab， 定义自动运行的任务。/etc/fstab，包含存储设备的列表，以及与他们相关的挂载点。/etc/passwd，包含用户帐号列表。 |
| /home          | 在通常的配置环境下，系统会在/home 下，给每个用户分配一个目录。普通用户只能 在自己的目录下写文件。这个限制保护系统免受错误的用户活动破坏。 |
| /lib           | 包含核心系统程序所使用的共享库文件。这些文件与 Windows 中的动态链接库相似。 |
| /lost+found    | 每个使用 Linux 文件系统的格式化分区或设备，例如 ext3文件系统， 都会有这个目录。当部分恢复一个损坏的文件系统时，会用到这个目录。这个目录应该是空的，除非文件系统 真正的损坏了。 |
| /media         | 在现在的 Linux 系统中，/media 目录会包含可移动介质的挂载点， 例如 USB 驱动器，CD-ROMs 等等。这些介质连接到计算机之后，会自动地挂载到这个目录结点下。 |
| /mnt           | 在早些的 Linux 系统中，/mnt 目录包含可移动介质的挂载点。     |
| /opt           | 这个/opt 目录被用来安装“可选的”软件。这个主要用来存储可能 安装在系统中的商业软件产品。 |
| /proc          | 这个/proc 目录很特殊。从存储在硬盘上的文件的意义上说，它不是真正的文件系统。 相反，它是一个由 Linux 内核维护的虚拟文件系统。它所包含的文件是内核的窥视孔。这些文件是可读的， 它们会告诉你内核是怎样监管计算机的。 |
| /root          | root 帐户的家目录。                                          |
| /sbin          | 这个目录包含“系统”二进制文件。它们是完成重大系统任务的程序，通常为超级用户保留。 |
| /tmp           | 这个/tmp 目录，是用来存储由各种程序创建的临时文件的地方。一些配置导致系统每次 重新启动时，都会清空这个目录。 |
| /usr           | 在 Linux 系统中，/usr 目录可能是最大的一个。它包含普通用户所需要的所有程序和文件。  现在usr被称为是**Unix System Resource**，即Unix系统资源的缩写。 |
| /usr/bin       | /usr/bin 目录包含系统安装的可执行程序。通常，这个目录会包含许多程序。 |
| /usr/lib       | 包含由/usr/bin 目录中的程序所用的共享库。                    |
| /usr/local     | 这个/usr/local 目录，是非系统发行版自带程序的安装目录。 通常，由源码编译的程序会安装在/usr/local/bin 目录下。新安装的 Linux 系统中会存在这个目录， 并且在管理员安装程序之前，这个目录是空的。 |
| /usr/sbin      | 包含许多系统管理程序。                                       |
| /usr/share     | /usr/share 目录包含许多由/usr/bin 目录中的程序使用的共享数据。 其中包括像默认的配置文件、图标、桌面背景、音频文件等等。 |
| /usr/share/doc | 大多数安装在系统中的软件包会包含一些文档。在/usr/share/doc 目录下， 我们可以找到按照软件包分类的文档。 |
| /var           | 除了/tmp 和/home 目录之外，相对来说，目前我们看到的目录是静态的，这是说， 它们的内容不会改变。/var 目录存放的是动态文件。各种数据库，假脱机文件， 用户邮件等等，都位于在这里。 |
| /var/log       | 这个/var/log 目录包含日志文件、各种系统活动的记录。这些文件非常重要，并且 应该时时监测它们。其中最重要的一个文件是/var/log/messages。注意，为了系统安全，在一些系统中， 你必须是超级用户才能查看这些日志文件。 |

### Linux 软件安装到 /usr，/usr/local/ 还是 /opt 目录？

Linux 的软件安装目录是也是有讲究的，理解这一点，在对系统管理是有益的

/usr：系统级的目录，可以理解为C:/Windows/，/usr/lib理解为C:/Windows/System32。

/usr/local：用户级的程序目录，可以理解为C:/Progrem Files/。用户自己编译的软件默认会安装到这个目录下。

/opt：用户级的程序目录，可以理解为D:/Software，opt有可选的意思，这里可以用于放置第三方大型软件（或游戏），当你不需要时，直接rm -rf掉即可。在硬盘容量不够时，也可将/opt单独挂载到其他磁盘上使用。

源码放哪里？

/usr/src：系统级的源码目录。

/usr/local/src：用户级的源码目录。

-----------------翻译-------------------

**/opt**

> Here’s where optional stuff is put. Trying out the latest Firefox beta? Install it to /opt where you can delete it without affecting other settings. Programs in here usually live inside a single folder whick contains all of their data, libraries, etc.
>
> 这里主要存放那些可选的程序。你想尝试最新的firefox测试版吗?那就装到/opt目录下吧，这样，当你尝试完，想删掉firefox的时候，你就可 以直接删除它，而不影响系统其他任何设置。安装到/opt目录下的程序，它所有的数据、库文件等等都是放在同个目录下面。
>
> 举个例子：刚才装的测试版firefox，就可以装到/opt/firefox_beta目录下，/opt/firefox_beta目录下面就包含了运 行firefox所需要的所有文件、库、数据等等。要删除firefox的时候，你只需删除/opt/firefox_beta目录即可，非常简单。

***\*/usr/local\****

> This is where most manually installed(ie. outside of your package manager) software goes. It has the same structure as /usr. It is a good idea to leave /usr to your package manager and put any custom scripts and things into /usr/local, since nothing important normally lives in /usr/local.
>
> 这里主要存放那些手动安装的软件，即不是通过“新立得”或apt-get安装的软件。它和/usr目录具有相类似的目录结构。让软件包管理器来管理/usr目录，而把自定义的脚本(scripts)放到/usr/local目录下面，我想这应该是个不错的主意。



## 文件

```shell
-rw-r--r-- 1 root root 3576296 2007-04-03 11:05 Experience ubuntu.ogg
-rw-r--r-- 1 root root 1186219 2007-04-03 11:05 kubuntu-leaflet.png
-rw-r--r-- 1 root root   47584 2007-04-03 11:05 logo-Edubuntu.png
-rw-r--r-- 1 root root   44355 2007-04-03 11:05 logo-Kubuntu.png
-rw-r--r-- 1 root root   34391 2007-04-03 11:05 logo-Ubuntu.png
-rw-r--r-- 1 root root   32059 2007-04-03 11:05 oo-cd-cover.odf
-rw-r--r-- 1 root root  159744 2007-04-03 11:05 oo-derivatives.doc
-rw-r--r-- 1 root root   27837 2007-04-03 11:05 oo-maxwell.odt
-rw-r--r-- 1 root root   98816 2007-04-03 11:05 oo-trig.xls
-rw-r--r-- 1 root root  453764 2007-04-03 11:05 oo-welcome.odt
-rw-r--r-- 1 root root  358374 2007-04-03 11:05 ubuntu Sax.ogg
```

| 字段             | 含义                                                         |
| :--------------- | :----------------------------------------------------------- |
| -rw-r--r--       | 对于文件的访问权限。第一个字符指明文件类型。在不同类型之间， 开头的“**－**”说明是一个普通文件，“**d**”表明是一个目录。"**b**" block 硬盘磁盘 "**c**" character  串行设备例如键盘、鼠标  "**s**" sockets 网络  "**l**" link 软连接 。其后三个字符是文件所有者的 访问权限，再其后的三个字符是文件所属组中成员的访问权限，最后三个字符是其他所 有人的访问权限。这个字段的完整含义将在第十章讨论。 |
| 1                | 文件的硬链接数目。参考随后讨论的关于链接的内容。             |
| root             | 文件所有者的用户名。                                         |
| root             | 文件所属用户组的名字。                                       |
| 32059            | 以字节数表示的文件大小。                                     |
| 2007-04-03 11:05 | 上次修改文件的时间和日期。                                   |
| oo-cd-cover.odf  | 文件名。                                                     |



文件类型

| 属性 | 文件类型                                                     |
| :--- | :----------------------------------------------------------- |
| -    | 一个普通文件                                                 |
| d    | 一个目录                                                     |
| l    | 一个符号链接。注意对于符号链接文件，剩余的文件属性总是"rwxrwxrwx"，而且都是 虚拟值。真正的文件属性是指符号链接所指向的文件的属性。 |
| c    | 一个字符设备文件。这种文件类型是指按照字节流来处理数据的设备。 比如说终端机或者调制解调器 |
| b    | 一个块设备文件。这种文件类型是指按照数据块来处理数据的设备，例如一个硬盘或者 CD-ROM 盘。 |

剩下的九个字符叫做文件模式，代表着文件所有者、文件组所有者和其他人的读、写和执行权限。

![](https://raw.githubusercontent.com/geekzsp/ImagesRepository/master/007S8ZIlly1ge2ozan089j30b2034gli.jpg)

| 属性 | 文件                                                         | 目录                                                         |
| :--- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| r    | 允许打开并读取文件内容。                                     | 允许列出目录中的内容，前提是目录必须设置了可执行属性（x）。  |
| w    | 允许写入文件内容或截断文件。但是不允许对文件进行重命名或删除，重命名或删除是由目录的属性决定的。 | 允许在目录下新建、删除或重命名文件，前提是目录必须设置了可执行属性（x）。 |
| x    | 允许将文件作为程序来执行，使用脚本语言编写的程序必须设置为可读才能被执行。 | 允许进入目录，例如：cd directory 。                          |

lrwxrwxrwx  符号链接的权限，符号链接的权限都是虚拟的，真实的权限应该以符号链接指向的文件为准。

#### 硬链接与符号链接

1. 一个硬链接不能关联它所在文件系统之外的文件。这是说一个链接不能关联 与链接本身不在同一个磁盘分区上的文件。
2. 一个硬链接不能关联一个目录。

当你删掉了其中一个文档的时候，是对另一个没有影响。但是 由于硬链接有不可以垮文件系统，不能为目录创建等限制，因此使用较少。



符号链接和 Windows 的快捷方式差不多，当然，符号链接早于 Windows 的快捷方式 很多年;-)一个符号链接指向一个文件，而且这个符号链接本身与其它的符号链接几乎没有区别。 例如，如果你往一个符号链接里面写入东西，那么相关联的文件也被写入。然而， 当你删除一个符号链接时，只有这个链接被删除，而不是文件自身。如果先于符号链接 删除文件，这个链接仍然存在，但是不指向任何东西。在这种情况下，这个链接被称为 坏链接。在许多实现中，ls 命令会以不同的颜色展示坏链接，比如说红色，来显示它们 的存在。

#### 查找文件

##### locate - 查找文件的简单方法

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ locate bin/z
/bin/zcat
/bin/zcmp
/bin/zdiff
/bin/zegrep
/bin/zfgrep
/bin/zforce
/bin/zgrep
/bin/zless
/bin/zmore
/bin/znew
/usr/bin/zdump
/usr/bin/zipdetails
```

你可能注意到了，在一些发行版中，仅仅在系统安装之后，locate 不能工作， 但是如果你第二天再试一下，它就正常工作了。怎么回事呢？locate 数据库由另一个叫做 updatedb 的程序创建。通常，这个程序作为一个定时任务（jobs）周期性运转；也就是说，一个任务 在特定的时间间隔内被 cron 守护进程执行。大多数装有 locate 的系统会每隔一天运行一回 updatedb 程序。因为数据库不能被持续地更新，所以当使用 locate 时，你会发现 目前最新的文件不会出现。为了克服这个问题，通过更改为超级用户身份，在提示符下运行 `updatedb` 命令， 可以手动运行 updatedb 程序

##### find - 查找文件的复杂方式

locate 程序只能依据文件名来查找文件，而 find 程序能基于各种各样的属性 搜索一个给定目录（以及它的子目录），来查找文件。我们将要花费大量的时间学习 find 命令

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ find ~ -type f
/home/vagrant/.bash_logout
/home/vagrant/test1.txt
/home/vagrant/.bashrc
/home/vagrant/test.txt
/home/vagrant/a.txt
/home/vagrant/.bash_history
/home/vagrant/.config/htop/htoprc
/home/vagrant/.viminfo
/home/vagrant/test2.txt
/home/vagrant/.ssh/authorized_keys
/home/vagrant/.cache/motd.legal-displayed
/home/vagrant/.profile
```

| 文件类型 | 描述             |
| :------- | :--------------- |
| b        | 块特殊设备文件   |
| c        | 字符特殊设备文件 |
| d        | 目录             |
| f        | 普通文件         |
| l        | 符号链接         |

我们也可以通过加入一些额外的测试条件，根据文件大小和文件名来搜索：让我们查找所有文件名匹配 通配符模式“*.JPG”和文件大小大于1M 的普通文件：

```shell
[me@linuxbox ~]$ find ~ -type f -name "*.JPG" -size +1M | wc -l
840
```



## 命令行开篇

一说到命令行，我们真正指的是 shell。shell 就是一个程序，它接受从键盘输入的命令， 然后把命令传递给操作系统去执行。几乎所有的 Linux 发行版都提供一个名为 bash 的 来自 GNU 项目的 shell 程序。“bash” 是 “Bourne Again SHell” 的首字母缩写， 所指的是这样一个事实，bash 是最初 Unix 上由 Steve Bourne 写成 shell 程序 sh 的增强版。



当使用图形用户界面时，我们需要另一个和 shell 交互的叫做终端仿真器的程序。 如果我们浏览一下桌面菜单，可能会找到一个。虽然在菜单里它可能都 被简单地称为 “terminal”，但是 KDE 用的是 konsole , 而 GNOME 则使用 gnome-terminal。 还有其他一些终端仿真器可供 Linux 使用，但基本上，它们都完成同样的事情， 让我们能访问 shell。也许，你可能会因为附加的一系列花俏功能而喜欢上某个终端。



### 查找命令所在目录的几种方式

```shell
[root@iZa2dj4ztavkc2jd3yea07Z ~]## type ifconfig
ifconfig 是 /usr/sbin/ifconfig

[root@iZa2dj4ztavkc2jd3yea07Z ~]## whereis ifconfig
ifconfig: /usr/sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz

[root@iZa2dj4ztavkc2jd3yea07Z ~]## which ifconfig
/usr/sbin/ifconfig
```

### Linux命令行参数前加双杠--,单杠-和不加杠-的区别



* 1 双杠与单杠的区别
  首先我们来看看一些实例来帮助我们理解，如下：

```shell
rm -vf ***

tar -xzvf  ***.tar.gz

gcc --version

rm --help
```

　　从上面命令我们可以看出，绝大数命令有以下的规则：
　　①　参数前单杠的表明后面的参数是字符形式；
　　②　参数前双杠的则表明后面的参数是单词形式。

* 2 加杠与不加杠的区别
  首先还是一样，我们看两个小样例：

```shell
tar xzvf  ***.tar.gz

tar -xzvf ***.tar.gz
```

　　两种命令行都是行的通的，并且功能都是解压软件包，那它们到底有什么不同呢，实际上这就涉及两种Linux风格，System V和BSD。它们对应关系如下：
　　**①　参数前有横的是System V风格。**
　　**②　参数前没有横的是BSD风格。**
　　System V和BSD两种风格的区别主要是：
　　系统启动过程中 kernel 最后一步调用的是 init 程序，init 程序的执行有两种风格，即 System V 和 BSD。
　　System V 风格中 init 调用 /etc/inittab，BSD 风格调用 /etc/rc，它们的目的相同，都是根据 runlevel 执行一系列的程序。

## linux shell 多个命令一起执行的几种方法

在命令行可以一次执行多个命令，有以下几种：

1.每个命令之间用;隔开
说明：各命令的执行结果，不会影响其它命令的执行。换句话说，各个命令都会执行，
但不保证每个命令都执行成功。

```shell
cd /home/PyTest/src; python suning.py1
```

2.每个命令之间用&&隔开
说明：若前面的命令执行成功，才会去执行后面的命令。这样可以保证所有的命令执行完毕后，执行过程都是成功的。

```shell
cd /home/PyTest/src&&python suning.py1
```

3.每个命令之间用||或者|隔开
说明：||是或的意思，只有前面的命令执行失败后才去执行下一条命令，直到执行成功
一条命令为止。

> **管道**可以将一个命令的输出导向另一个命令的输入，从而让两个(或者更多命令)像流水线一样连续工作，不断地处理文本流。在命令行中，我们用|表示管道

```shell
cd /home/PyTest/123 || echo "error234"
cd /home/PyTest/123 | echo "error234"
```

**command1 & command2 & command3   三个命令同时执行** 

**command1; command2; command3      不管前面命令执行成功没有，后面的命令继续执行** 

**command1 && command2             只有前面命令执行成功，后面命令才继续执行**



## 重定向

与 Unix 主题“任何东西都是一个文件”保持一致，像 ls这样的程序实际上把他们的运行结果 输送到一个叫做标准输出的特殊文件（经常用 **stdout** 表示），而它们的状态信息则送到另一个 叫做标准错误的文件（**stderr**）。默认情况下，标准输出和标准错误都连接到屏幕，而不是 保存到磁盘文件。除此之外，许多程序从一个叫做标准输入（**stdin**）的设备得到输入，默认情况下， 标准输入连接到键盘。

I/O 重定向允许我们更改输出地点和输入来源。一般来说，输入来自键盘，输出送到屏幕， 但是通过 I/O 重定向，我们可以做出改变。

#### 标准输出重定向

```shell
echo a> a.txt
## 可以清空 或者新建文件
> a.txt 
## 追加写入
echo b >> a.txt
```

#### 标准错误重定向

标准错误重定向没有专用的重定向操作符。为了重定向标准错误，我们必须参考其文件描述符。 一个程序可以在几个编号的文件流中的任一个上产生输出。虽然我们已经将这些文件流的前 三个称作标准输入、输出和错误，shell 内部分别将其称为文件描述符**0、1和2**。shell 使用文件描述符提供 了一种表示法来重定向文件。因为标准错误和文件描述符2一样，我们用这种 表示法来重定向标准错误：

```shell
ls /a 2> a.txt
```

文件描述符”2”，紧挨着放在重定向操作符之前，来执行重定向标准错误到文件 ls-error.txt 任务。

#### 重定向标准输出和错误到同一个文件

##### 方式1 旧版shell

```shell
ls -l /bin/usr > ls-output.txt 2>&1
```

使用这种方法，我们完成两个重定向。首先重定向标准输出到文件 ls-output.txt，然后 重定向文件描述符2（标准错误）到文件描述符1（标准输出）使用表示法2>&1。

##### 方式2 新版shell

```shel
ls -l /bin/usr &> ls-output.txt
```

我们使用单单一个表示法 &> 来重定向标准输出和错误到文件 ls-output.txt

#### 处理不需要的输出

系统通过重定向输出结果到一个叫做**”/dev/null”**的特殊文件， 为我们提供了解决问题的方法。这个文件是系统设备，叫做位存储桶，它可以 接受输入，并且对输入不做任何处理

```she
ls -l /bin/usr 2> /dev/null
```

#### 标准输入重定向

```shell
cat < a.txt
```

使用文件内容替代标准输入 显示到屏幕上

#### 管道线

command 1 | command 2 他的功能是把第一个命令command 1执行的结果作为command 2的输入传给command 2

```shell
command1 | command2
ls -l /usr/bin | less
```





## 文本相关命令

####  wc（字计数）命令是用来显示文件所包含的行数、字数和字节数

```shell
root@OpenWrt:/## wc b.txt
       20        20        89 b.txt
```

#### grep － 打印匹配行



#### head / tail － 打印文件开头部分/结尾部分

有时候你不需要一个命令的所有输出。可能你只想要前几行或者后几行的输出内容。 head 命令打印文件的前十行，而 tail 命令打印文件的后十行。默认情况下，两个命令 都打印十行文本，但是可以通过”-n”选项来调整命令打印的行数。

```shell
head -n 5 ls-output.txt
```

```shell
root@OpenWrt:/## ls / | head -n 2
bin
boot
```

#### Less is  More

less 程序是早期 Unix 程序 more 的改进版。“less” 这个名字，对习语 “**less is more**” 开了个玩笑， 这个习语是现代主义建筑师和设计者的座右铭。

less 属于”页面调度器”类程序，这些程序允许以逐页方式轻松浏览长文本文档。 more 程序只能向前翻页，而 less 程序允许前后翻页，此外还有很多其它的特性。

#### echo

```shell
root@OpenWrt:/tmp/log## ls
ddns          log.nmbd      minidlna.log  nginx
lastlog       log.smbd      netdata       wtmp
root@OpenWrt:/tmp/log## echo *
ddns lastlog log.nmbd log.smbd minidlna.log netdata nginx wtmp
root@OpenWrt:/tmp/log#
```

算术表达式展开

```shell
echo $((2 + 2))
4
```

算术表达式展开使用这种格式：

```
$((expression))
```

花括号展开

```shell
echo Front-{A,B,C}-Back
Front-A-Back Front-B-Back Front-C-Back
```

命令替换

命令替换允许我们把一个命令的输出作为一个展开模式来使用：

```shell
root@OpenWrt:/usr## echo $(ls)
bin lib lib64 libexec man sbin scgi_temp share uwsgi_temp
```

双引号

```shell
echo "The total is $100.00"
```

如果需要禁止所有的展开，我们要使用单引号

```shell
[me@linuxbox ~]$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/ls-output.txt a b foo 4 me
[me@linuxbox ~]$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text ~/*.txt   {a,b} foo 4 me
[me@linuxbox ~]$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt  {a,b} $(echo foo) $((2+2)) $USER
```

转义字符

有时候我们只想引用单个字符。我们可以在字符之前加上一个反斜杠，在这里叫做转义字符。 经常在双引号中使用转义字符，来有选择地阻止展开。

```shell
[me@linuxbox ~]$ echo "The balance for user $USER is: \$5.00"
The balance for user me is: $5.00
```





## 键盘高级技巧

| 按键   | 行动                                                       |
| :----- | :--------------------------------------------------------- |
| Ctrl-a | 移动光标到行首。                                           |
| Ctrl-e | 移动光标到行尾。                                           |
| Ctrl-l | 清空屏幕，移动光标到左上角。**clear** 命令完成同样的工作。 |

| 序列     | 行为                                                         |
| :------- | :----------------------------------------------------------- |
| !!       | 重复最后一次执行的命令。可能按下上箭头按键和 enter 键更容易些。 |
| !number  | 重复历史列表中第 number 行的命令。                           |
| !string  | 重复最近历史列表中，以这个字符串开头的命令。                 |
| !?string | 重复最近历史列表中，包含这个字符串的命令。                   |



## 权限



Unix 传统中的操作系统不同于那些 MS-DOS 传统中的系统，区别在于它们不仅是多任务系统，而且也是 **多用户系统**。这到底意味着什么？它意味着多个用户可以在同一时间使用同一台计算机。然而一个 典型的计算机可能只有一个键盘和一个监视器，但是它仍然可以被多个用户使用。例如，如果一台 计算机连接到一个网络或者因特网，那么远程用户通过 ssh（安全 shell）可以登录并操纵这台电脑。 事实上，远程用户也能运行图形界面应用程序，并且图形化的输出结果会出现在远端的显示器上。 X 窗口系统把这个作为基本设计理念的一部分，并支持这种功能。



让我们看一下输出结果。当用户创建帐户之后，系统会给用户分配一个号码，叫做用户 ID 或者 uid，然后，为了符合人类的习惯，这个 ID 映射到一个用户名。系统又会给这个用户 分配一个原始的组 ID(即 gid)。一个用户可以属于额外的组(除gid外,有更多的组)

####  id 命令，来找到关于你自己身份的信息：

```shell
[me@linuxbox ~]$ id
uid=500(me) gid=500(me) groups=500(me)
```

那么这些信息来源于哪里呢？像 Linux 系统中的许多东西一样，来自一系列的文本文件。用户帐户 定义在/etc/passwd 文件里面，用户组定义在/etc/group 文件里面。当用户帐户和用户组创建以后， 这些文件随着文件/etc/shadow 的变动而修改，文件/etc/shadow 包含了关于用户密码的信息。 对于每个用户帐号，文件/etc/passwd 定义了用户（登录）名、uid、gid、帐号的真实姓名、家目录 和登录 shell。如果你查看一下文件/etc/passwd 和文件/etc/group 的内容，你会注意到除了普通 用户帐号之外，还有超级用户（uid 0）帐号，和各种各样的系统用户。



#### chmod － 更改文件模式

| Octal | Binary | File Mode |
| ----- | ------ | --------- |
| 0     | 000    | ---       |
| 1     | 001    | --x       |
| 2     | 010    | -w-       |
| 3     | 011    | -wx       |
| 4     | 100    | r--       |
| 5     | 101    | r-x       |
| 6     | 110    | rw-       |
| 7     | 111    | rwx       |

#### su － 以其他用户身份和组 ID 运行一个 shell

#### sudo － 以另一个用户身份执行命令

sudo 命令在很多方面都相似于 su 命令，但是 sudo 还有一些非常重要的功能。管理员能够配置 sudo 命令，从而允许一个普通用户以不同的身份（通常是超级用户），通过一种非常可控的方式 来执行命令。尤其是，只有一个用户可以执行一个或多个特殊命令时，（更体现了 sudo 命令的方便性）。 另一个重要差异是 sudo 命令不要求超级用户的密码。使用 sudo 命令时，用户使用他/她自己的密码 来认证。比如说，例如，sudo 命令经过配置，允许我们运行一个虚构的备份程序，叫做”backup_script”， 这个程序要求超级用户权限。通过 sudo 命令，这个程序会像这样运行：

```shell
[me@linuxbox ~]$ sudo backup_script
Password:
System Backup Starting...
```

按下回车键之后，shell 提示我们输入我们的密码（不是超级用户的）。一旦认证完成，则执行 具体的命令。su 和 sudo 之间的一个重要区别是 sudo 不会重新启动一个 shell，也不会加载另一个 用户的 shell 运行环境。这意味者命令不必用单引号引起来。注意通过指定各种各样的选项，这 种行为可以被推翻。详细信息，阅读 sudo 手册页。

#### chown － 更改文件所有者和用户组

#### passwd 更改用户密码 



## 内存

如果你看一下 free 命令的输出结果，这个命令用来显示关于内存使用情况的统计信息，你 会看到一个统计值叫做”buffers“。计算机系统旨在尽可能快地运行。系统运行速度的 一个阻碍是缓慢的设备。打印机是一个很好的例子。即使最快速的打印机相比于计算机标准也 极其地缓慢。一台计算机确实会运行得非常慢，如果它要停下来等待一台打印机打印完一页。 在早期的个人电脑时代（多任务之前），这真是个问题。如果你正在编辑电子表格 或者是文本文档，每次你要打印文件时，计算机都会停下来而且变得不能使用。 计算机能以打印机可接受的最快速度把数据发送给打印机，但由于打印机不能快速地打印， 这个发送速度会非常慢。由于打印机缓存的出现，这个问题被解决了。**打印机缓存是一个包含一些 RAM 内存 的设备，位于计算机和打印机之间。通过打印机缓存，计算机把要打印的结果发送到这个缓存区， 数据会迅速地存储到这个 RAM 中，这样计算机就能回去工作，而不用等待。与此同时，打印机缓存将会 以打印机可接受的速度把缓存中的数据缓慢地输出给打印机**。



缓存被广泛地应用于计算机中，使其运行得更快。别让偶尔地的读取或写入慢设备的需求阻碍了 系统的运行速度。在真正与比较慢的设备交互之前，操作系统会尽可能多的读取或写入数据到内存中的 存储设备里。以 Linux 操作系统为例，你会注意到系统看似填充了多于它所需要的内存。 这不意味着 Linux 正在使用所有的内存，它意味着 Linux 正在利用所有可用的内存，来作为缓存区。

这个缓存区允许非常快速地对存储设备进行写入，因为写入物理设备的操作被延迟到后面进行。同时， 这些注定要传送到设备中的数据正在内存中堆积起来。时不时地，操作系统会把这些数据 写入物理设备。



卸载一个设备需要把所有剩余的数据写入这个设备，所以设备可以被安全地移除。如果 没有卸载设备，就移除了它，就有可能没有把注定要发送到设备中的数据输送完毕。在某些情况下， 这些数据可能包含重要的目录更新信息，这将导致文件系统损坏，这是发生在计算机中的最坏的事情之一。

## 进程

通常，现在的操作系统都支持多任务，意味着操作系统通过在一个执行中的程序和另一个 程序之间快速地切换造成了一种它同时能够做多件事情的假象。Linux 内核通过使用进程来 管理多任务。进程，就是Linux 组织安排正在等待使用 CPU的各种程序的方式。

![image-20200423113630729](https://raw.githubusercontent.com/geekzsp/ImagesRepository/master/EbJQLez.jpg)

当系统启动的时候，内核先把一些它自己的活动初始化为进程，然后运行一个叫做 **init** 的程序。init， 依次地，再运行一系列的称为 init 脚本的 shell 脚本（位于/etc/init.d），它们可以启动所有的系统服务。 其中许多系统服务以守护（daemon）程序的形式实现，守护程序仅在后台运行，没有任何用户接口(User Interface)。 这样，即使我们没有登录系统，至少系统也在忙于执行一些例行事务。

内核维护每个进程的信息，以此来保持事情有序。例如，系统分配给每个进程一个数字，这个数字叫做 进程(process) ID 或 PID。PID 号按升序分配，**init 进程的 PID 总是1**。内核也对分配给每个进程的内存和就绪状态进行跟踪以便继续执行这个进程。 像文件一样，进程也有所有者和用户 ID，有效用户 ID，等等。

#### ps 

> Process status

它最简单地使用形式是这样的：

```shell
vagrant@vagrant-ubuntu-trusty-64:/$ ps
  PID TTY          TIME CMD
 1915 pts/0    00:00:00 bash
 2087 pts/0    00:00:00 ps
```

ps 不会显示很多进程信息，只是列出与当前终端会话相关的进程。 TTY 是 “Teletype”(直译电传打字机) 的简写，是指进程的控制终端。TTY足足显示了 Unix 的年代久远。TIME 字段表示 进程所消耗的 CPU 时间数量

如果给 ps 命令加上选项，我们可以得到更多关于系统运行状态的信息：

```shell
vagrant@vagrant-ubuntu-trusty-64:/$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.1  0.5  33564  2920 ?        Ss   07:43   0:00 /sbin/init
root         2  0.0  0.0      0     0 ?        S    07:43   0:00 [kthreadd]
root         3  0.0  0.0      0     0 ?        S    07:43   0:00 [ksoftirqd/0]
root         4  0.0  0.0      0     0 ?        S    07:43   0:00 [kworker/0:0]
root         5  0.0  0.0      0     0 ?        S<   07:43   0:00 [kworker/0:0H]
root         7  0.0  0.0      0     0 ?        S    07:43   0:00 [rcu_sched]
root         8  0.0  0.0      0     0 ?        S    07:43   0:00 [rcuos/0]
root         9  0.0  0.0      0     0 ?        S    07:43   0:00 [rcu_bh]
root        10  0.0  0.0      0     0 ?        S    07:43   0:00 [rcuob/0]
root        11  0.0  0.0      0     0 ?        S    07:43   0:00 [migration/0]
```

Sats 进程状态

| 状态 | 含义                                                         |
| :--- | :----------------------------------------------------------- |
| R    | 运行中。这意味着，进程正在运行或准备运行。                   |
| S    | 正在睡眠。进程没有运行，而是，正在等待一个事件， 比如说，一个按键或者网络分组。 |
| D    | 不可中断睡眠。进程正在等待 I/O，比方说，一个磁盘驱动器的 I/O。 |
| T    | 已停止. 已经指示进程停止运行。稍后介绍更多。                 |
| Z    | 一个死进程或“僵尸”进程。这是一个已经终止的子进程，但是它的父进程还没有清空它。 （父进程没有把子进程从进程表中删除） |
| <    | 一个高优先级进程。这可能会授予一个进程更多重要的资源，给它更多的 CPU 时间。 进程的这种属性叫做 niceness。具有高优先级的进程据说是不好的（less nice）， 因为它占用了比较多的 CPU 时间，这样就给其它进程留下很少时间。 |
| N    | 低优先级进程。 一个低优先级进程（一个“nice”进程）只有当其它高优先级进程被服务了之后，才会得到处理器时间。 |

#### top

虽然 ps 命令能够展示许多计算机运行状态的信息，但是它只是提供 ps 命令执行时刻的机器状态快照。 为了看到更多动态的信息，我们使用 top 命令：

top 程序以进程活动顺序显示连续更新的系统进程列表。（默认情况下，每三秒钟更新一次），”top”这个名字 来源于 top 程序是用来查看系统中“顶端”进程的。top 显示结果由两部分组成： 最上面是系统概要，下面是进程列表，以 CPU 的使用率排序。

```shell
top - 14:59:20 up 6:30, 2 users, load average: 0.07, 0.02, 0.00
Tasks: 109 total,   1 running,  106 sleeping,    0 stopped,    2 zombie
Cpu(s): 0.7%us, 1.0%sy, 0.0%ni, 98.3%id, 0.0%wa, 0.0%hi, 0.0%si
Mem:   319496k total,   314860k used,   4636k free,   19392k buff
Swap:  875500k total,   149128k used,   726372k free,  114676k cach

 PID  USER       PR   NI   VIRT   RES   SHR  S %CPU  %MEM   TIME+    COMMAND
6244  me         39   19  31752  3124  2188  S  6.3   1.0   16:24.42 trackerd
....
```

| 行号 | 字段          | 意义                                                         |
| :--- | :------------ | :----------------------------------------------------------- |
| 1    | top           | 程序名。                                                     |
|      | 14:59:20      | 当前时间。                                                   |
|      | up 6:30       | 这是正常运行时间。它是计算机从上次启动到现在所运行的时间。 在这个例子里，系统已经运行了六个半小时。 |
|      | 2 users       | 有两个用户登录系统。                                         |
|      | load average: | 加载平均值是指，等待运行的进程数目，也就是说，处于可以运行状态并共享 CPU 的进程个数。 这里展示了三个数值，每个数值对应不同的时间段。第一个是最后60秒的平均值， 下一个是前5分钟的平均值，最后一个是前15分钟的平均值。若平均值低于1.0，则指示计算机 工作不忙碌。 |
| 2    | Tasks:        | 总结了进程数目和这些进程的各种状态。                         |
| 3    | Cpu(s):       | 这一行描述了 CPU 正在进行的活动的特性。                      |
|      | 0.7%us        | 0.7% 的 CPU 被用于用户进程。这意味着进程在内核之外。         |
|      | 1.0%sy        | 1.0%的 CPU 时间被用于系统（内核）进程。                      |
|      | 0.0%ni        | 0.0%的 CPU 时间被用于"nice"（低优先级）进程。                |
|      | 98.3%id       | 98.3%的 CPU 时间是空闲的。                                   |
|      | 0.0%wa        | 0.0%的 CPU 时间来等待 I/O。                                  |
| 4    | Mem:          | 展示物理内存的使用情况。                                     |
| 5    | Swap:         | 展示交换分区（虚拟内存）的使用情况。                         |

![WX20190319-102501@2x](https://raw.githubusercontent.com/geekzsp/ImagesRepository/master/007S8ZIlly1ge3jq72jydj31de0kmtrb.jpg)

**命令选项**

* c 参考详细命令
* 1 查看多核 多cpu
* t 切换cpu视图
* m 切换memory视图
* b 当前运行的进程
* x 高亮排序 默认 cpu  `shift +<|>`左右移动排序规则
* s 刷新间隔 秒

扩展命令htop



#### Kill

​	

虽然这个命令看上去很直白， 但是它的含义不止于此。这个 kill 命令不是真的“杀死”程序，而是给程序 发送**信号**。信号是操作系统与程序之间进行通信时所采用的几种方式中的一种。 在使用 Ctrl-c 和 Ctrl-z 的过程中我们已经看到信号的实际用法。当终端接受了其中一个按键组合后，它会给在前端运行 的程序发送一个信号。在使用 Ctrl-c 的情况下，会发送一个叫做 INT（Interrupt,中断）的信号；当使用 Ctrl-z 时，则发送一个叫做 TSTP（Terminal Stop,终端停止）的信号。程序，相应地，监听信号的到来，当程序 接到信号之后，则做出响应。一个程序能够监听和响应信号这件事允许一个程序做些事情， 比如，当程序接到一个终止信号时，它可以保存所做的工作。

```shell
kill [-signal] PID...
```

如果在命令行中没有指定信号，那么默认情况下，发送 TERM（Terminate，终止）信号。kill 命令被经常 用来发送以下命令：

| 编号 | 名字 | 含义                                                         |
| :--- | :--- | :----------------------------------------------------------- |
| 1    | HUP  | 挂起（Hangup）。这是美好往昔的残留部分，那时候终端机通过电话线和调制解调器连接到 远端的计算机。这个信号被用来告诉程序，控制的终端机已经“挂断”。 通过关闭一个终端会话，可以展示这个信号的作用。在当前终端运行的前台程序将会收到这个信号并终止。许多守护进程也使用这个信号，来重新初始化。这意味着，当一个守护进程收到这个信号后， 这个进程会重新启动，并且重新读取它的配置文件。Apache 网络服务器守护进程就是一个例子。 |
| 2    | INT  | 中断。实现和 Ctrl-c 一样的功能，由终端发送。通常，它会终止一个程序。 |
| 9    | KILL | 杀死。这个信号很特别。尽管程序可能会选择不同的方式来处理发送给它的 信号，其中也包含忽略信号，但是 KILL 信号从不被发送到目标程序。而是内核立即终止 这个进程。当一个进程以这种方式终止的时候，它没有机会去做些“清理”工作，或者是保存工作。 因为这个原因，把 KILL 信号看作最后一招，当其它终止信号失败后，再使用它。 |
| 15   | TERM | 终止。这是 kill 命令发送的默认信号。如果程序仍然“活着”，可以接受信号，那么 这个它会终止。 |
| 18   | CONT | 继续。在一个停止信号后，这个信号会恢复进程的运行。           |
| 19   | STOP | 停止。这个信号导致进程停止运行，而不是终止。像 KILL 信号，它不被 发送到目标进程，因此它不能被忽略。 |



#### nohup &

  &的意思是在后台运行， 什么意思呢？  意思是说， 当你在执行 ./a.out & 的时候， 即使你用ctrl C,  那么a.out照样运行（**因为对SIGINT信号免疫**）。 但是要注意， 如果你直接关掉shell后， 那么， a.out进程同样消失。 可见， &的后台并不硬（因为对SIGHUP信号不免疫）。

   **nohup的意思是忽略SIGHUP信号**， 所以当运行nohup ./a.out的时候， 关闭shell, 那么a.out进程还是存在的（对SIGHUP信号免疫）。 但是， 要注意， 如果你直接在shell中用Ctrl C, 那么, a.out进程也是会消失的（因为对SIGINT信号不免疫）

   所以， &和nohup没有半毛钱的关系， 要让进程真正不受shell中Ctrl C和shell关闭的影响， 那该怎么办呢？ 那就用nohua ./a.out &吧， 两全其美。

    如果你懂守护进程， 那么nohup ./a.out &颇有点让a.out成为守护进程的感觉。
    
    SIGHUP： 退出终端信号
    
    SIGINT：  程序终止信号

* 1. nohup

  用途：不挂断地运行命令。

  语法：nohup Command [ Arg … ] [　& ]

  　　无论是否将 nohup 命令的输出重定向到终端，输出都将附加到当前目录的 nohup.out 文件中。

  　　如果当前目录的 nohup.out 文件不可写，输出重定向到 $HOME/nohup.out 文件中。

  　　如果没有文件能创建或打开以用于追加，那么 Command 参数指定的命令不可调用。

  退出状态：该命令返回下列出口值： 　

  　　126 可以查找但不能调用 Command 参数指定的命令。 　

  　　127 nohup 命令发生错误或不能查找由 Command 参数指定的命令。 　

  　　否则，nohup 命令的退出状态是 Command 参数指定命令的退出状态。

* 2.&

  用途：在后台运行

  一般两个一起用

  nohup command &

  

## 环境变量



| 变量    | 内容                                                         |
| :------ | :----------------------------------------------------------- |
| DISPLAY | 如果你正在运行图形界面环境，那么这个变量就是你显示器的名字。通常，它是 ":0"， 意思是由 X 产生的第一个显示器。 |
| EDITOR  | 文本编辑器的名字。                                           |
| SHELL   | shell 程序的名字。                                           |
| HOME    | 用户家目录。                                                 |
| LANG    | 定义了字符集以及语言编码方式。                               |
| OLD_PWD | 先前的工作目录。                                             |
| PAGER   | 页输出程序的名字。这经常设置为/usr/bin/less。                |
| PATH    | 由冒号分开的目录列表，当你输入可执行程序名后，会搜索这个目录列表。 |
| PS1     | Prompt String 1. 这个定义了你的 shell 提示符的内容。随后我们可以看到，这个变量 内容可以全面地定制。 |
| PWD     | 当前工作目录。                                               |
| TERM    | 终端类型名。类 Unix 的系统支持许多终端协议；这个变量设置你的终端仿真器所用的协议。 |
| TZ      | 指定你所在的时区。大多数类 Unix 的系统按照协调时间时 (UTC) 来维护计算机内部的时钟 ，然后应用一个由这个变量指定的偏差来显示本地时间。 |
| USER    | 你的用户名                                                   |

我们可以用 bash 的内建命令 set，或者是 printenv 程序来查看环境变量。set 命令可以 显示 shell 或环境变量，而 **printenv 只是显示环境变量**。因为环境变量列表比较长，最好 把每个命令的输出通过管道传递给 less 来阅读：

```shell
vagrant@vagrant-ubuntu-trusty-64:/$ printenv | less
```

printenv 命令也能够列出特定变量的数值：

```shell
vagrant@vagrant-ubuntu-trusty-64:/$ printenv USER
vagrant
```

也可以通过 echo 命令来查看一个变量的内容

```shell
vagrant@vagrant-ubuntu-trusty-64:/$ echo $USER
vagrant
```

当使用没有带选项和参数的 set 命令时，shell 变量，环境变量，和定义的 shell 函数 都会被显示。不同于 printenv 命令，set 命令的输出很友好地按照首字母顺序排列：

```shell
[me@linuxbox ~]$ set | less
```

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ a=666
vagrant@vagrant-ubuntu-trusty-64:~$ exprot b=777
vagrant@vagrant-ubuntu-trusty-64:~$ unset a;unset b
```

别名**无法通过使用 set 或 printenv 来查看。 用不带参数的 alias 来查看别名:

```shell
vagrant@vagrant-ubuntu-trusty-64:/$ alias
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'
```

设置别名

```shell
alias foo='cd /usr; ls; cd -'
```



当我们登录系统后， bash 程序启动，并且会读取一系列称为启动文件的配置脚本， 这些文件定义了默认的可供所有用户共享的 shell 环境。然后是读取更多位于我们自己家目录中 的启动文件，这些启动文件定义了用户个人的 shell 环境。确切的启动顺序依赖于要运行的 shell 会话 类型。有两种 shell 会话类型：**一个是登录 shell 会话**，**另一个是非登录 shell 会话**。

*登录 shell 会话的启动文件*

| 文件            | 内容                                                         |
| :-------------- | :----------------------------------------------------------- |
| /etc/profile    | 应用于所有用户的全局配置脚本。                               |
| ~/.bash_profile | 用户个人的启动文件。可以用来扩展或重写全局配置脚本中的设置。 |
| ~/.bash_login   | 如果文件 ~/.bash_profile 没有找到，bash 会尝试读取这个脚本。 |
| ~/.profile      | 如果文件 ~/.bash_profile 或文件 ~/.bash_login 都没有找到，bash 会试图读取这个文件。 这是基于 Debian 发行版的默认设置，比方说 Ubuntu。 |

*非登录 shell 会话的启动文件*：

| 文件             | 内容                                                         |
| :--------------- | :----------------------------------------------------------- |
| /etc/bash.bashrc | 应用于所有用户的全局配置文件。                               |
| ~/.bashrc        | 用户个人的启动文件。可以用来扩展或重写全局配置脚本中的设置。 |



> 在普通用户看来，文件 ~/.bashrc 可能是最重要的启动文件，因为它几乎总是被读取。非登录 shell 默认 会读取它，并且大多数登录 shell 的启动文件会以能读取 ~/.bashrc 文件的方式来书写。

如果我们看一下典型的 .bash_profile 文件（来自于 CentOS 4 系统），它看起来像这样：

```
## .bash_profile
## Get the aliases and functions
if [ -f ~/.bashrc ]; then
. ~/.bashrc
fi
## User specific environment and startup programs
PATH=$PATH:$HOME/bin
export PATH
```



是否曾经对 shell 怎样知道在哪里找到我们在命令行中输入的命令感到迷惑？例如，当我们输入 ls 后， shell 不会查找整个计算机系统来找到 /bin/ls（ls 命令的全路径名），相反，它查找一个目录列表， 这些目录包含在 PATH 变量中。

```shell
export PATH=$HOME/bin:/usr/local/bin:$PATH
```

按照通常的规则，添加目录到你的 PATH 变量或者是定义额外的环境变量，要把这些更改放置到 .bash_profile 文件中（或者其替代文件中，根据不同的发行版。例如，Ubuntu 使用 .profile 文件）。 对于其它的更改，要放到 .bashrc 文件中。除非你是系统管理员，需要为系统中的所有用户修改 默认设置，那么则限定你只能对自己家目录下的文件进行修改。当然，有可能会更改 /etc 目录中的 文件，比如说 profile 文件，而且在许多情况下，修改这些文件也是明智的，但是现在，我们要谨慎行事。



我们对于文件 .bashrc 的修改不会生效，直到我们关闭终端会话，再重新启动一个新的会话， 因为 .bashrc 文件只是在刚开始启动终端会话时读取。然而，我们可以强迫 bash 重新读取修改过的 .bashrc 文件，使用下面的命令：

```shell
[me@linuxbox ~]$ source .bashrc
```

## VIM

* 插入模式  i 插入

* 命令模式

按键

| 按键                | 移动光标                                          |
| :------------------ | :------------------------------------------------ |
| l or 右箭头         | 向右移动一个字符                                  |
| h or 左箭头         | 向左移动一个字符                                  |
| j or 下箭头         | 向下移动一行                                      |
| k or 上箭头         | 向上移动一行                                      |
| **0 (零按键)**      | **移动到当前行的行首。**                          |
| ^                   | 移动到当前行的第一个非空字符。                    |
| **$**               | **移动到当前行的末尾。**                          |
| w                   | 移动到下一个单词或标点符号的开头。                |
| W                   | 移动到下一个单词的开头，忽略标点符号。            |
| b                   | 移动到上一个单词或标点符号的开头。                |
| B                   | 移动到上一个单词的开头，忽略标点符号。            |
| Ctrl-f or Page Down | 向下翻一页                                        |
| Ctrl-b or Page Up   | 向上翻一页                                        |
| numberG             | 移动到第 number 行。例如，1G 移动到文件的第一行。 |
| G                   | 移动到文件末尾。                                  |

| 命令  | 打开行                                                       |
| :---- | :----------------------------------------------------------- |
| **o** | **当前行的下方打开一行。**                                   |
| O     | 当前行的上方打开一行。                                       |
| A     | 因为我们几乎总是想要在行尾添加文本，所以 vi 提供了一个快捷键。光标将移动到行尾，同时 vi 进入输入模式。 它是**”A”**命令。试着用一下它，向文件添加更多行。 |

| 命令   | 删除的文本                               |
| :----- | :--------------------------------------- |
| x      | 当前字符                                 |
| 3x     | 当前字符及其后的两个字符。               |
| **dd** | **当前行。**                             |
| 5dd    | 当前行及随后的四行文本。                 |
| dW     | 从光标位置开始到下一个单词的开头。       |
| d$     | 从光标位置开始到当前行的行尾。           |
| d0     | 从光标位置开始到当前行的行首。           |
| d^     | 从光标位置开始到文本行的第一个非空字符。 |
| **dG** | **从当前行到文件的末尾。**               |
| d20G   | 从当前行到文件的第20行。                 |

| 命令 | 复制的内容                               |
| :--- | :--------------------------------------- |
| yy   | 当前行。                                 |
| 5yy  | 当前行及随后的四行文本。                 |
| yW   | 从当前光标位置到下一个单词的开头。       |
| y$   | 从当前光标位置到当前行的末尾。           |
| y0   | 从当前光标位置到行首。                   |
| y^   | 从当前光标位置到文本行的第一个非空字符。 |
| yG   | 从当前行到文件末尾。                     |
| y20G | 从当前行到文件的第20行。                 |

**查找和替换**

移动光标到下一个出现的单词或短语上，使用 / 命令。这个命令和我们之前在 less 程序中学到 的一样。当你输入/命令后，一个**”/”**字符会出现在屏幕底部。接下来，输入要查找的单词或短语， 按下回车。光标就会移动到下一个包含所查找字符串的位置。通过 n 命令来重复先前的查找。 这里有个例子：

**另存为**

这个:w 命令也可以指定可选的文件名。这个的作用就如”Save As…“。例如，如果我们 正在编辑 foo.txt 文件，想要保存一个副本，叫做 foo1.txt，那么我们可以执行以下命令：

```
:w foo1.txt
```



## 包管理器

不同的 Linux 发行版使用不同的打包系统，一般而言，大多数发行版分别属于两大包管理技术阵营： Debian 的”.deb”，和红帽的”.rpm”。也有一些重要的例外，比方说 Gentoo， Slackware，和 Foresight，但大多数会使用这两个基本系统中的一个。

| 包管理系统           | 发行版 (部分列表)                                            |
| :------------------- | :----------------------------------------------------------- |
| Debian Style (.deb)  | Debian, Ubuntu, Xandros, Linspire                            |
| Red Hat Style (.rpm) | Fedora, CentOS, Red Hat Enterprise Linux, OpenSUSE, Mandriva, PCLinuxOS |

interactive



## 存储媒介

```shell
#挂载一个文件系统
mkdir   /mnt/sda2
mount  /dev/sda2 /mnt/sda2
#卸载一个文件系统
umount /mnt/sda2
#检查和修复一个文件系统
fsck
## 分区表控制器
fdisk 
fdisk -l
#列出块设备信息
vagrant@vagrant-ubuntu-trusty-64:~$ lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sda      8:0    0  40G  0 disk
└─sda1   8:1    0  40G  0 part /
#把面向块的数据直接写入设备
#写入测试
time dd count=500 bs=1M if=/dev/zero of=test.test
#读取测试
time dd count=500 bs=1M if=test.test of=/dev/null
#测速
#服务端启动
iperf3 -s
#客户端启动 
iperf3 -c 192.168.2.1
```



管理存储设备的第一步是把设备连接到文件系统树中。这个叫做”挂载”的过程允许设备连接到操作系统中。 回想一下第三章，类 Unix 的操作系统，比如Linux在单一文件系统树中维护连接在各个节点的各种设备。 这与其它操作系统形成对照，比如说 MS-DOS 和 Windows 系统中，每个设备（例如 C:\，D:\，等） 保持着单独的文件系统树。

注意(类 Unix 系统)不像 Windows ，每个存储设备都有一个独自的文件系统。类 Unix 操作系统， 比如 Linux，总是**只有一个单一的文件系统树**，不管有多少个磁盘或者存储设备连接到计算机上。 根据负责维护系统安全的系统管理员的兴致，存储设备连接到（或着更精确些，是挂载到）目录树的各个节点上。



> 事实上，在类 Unix 操作系统中比如说 Linux 中，有个普遍的观念就是“**一切皆文件**”。 随着课程的进行，我们将会明白这句话是多么的正确。



有一个叫做`/etc/fstab` 的文件可以列出系统启动时要挂载的设备（典型地，硬盘分区）。

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ cat /etc/fstab
LABEL=cloudimg-rootfs	/	 ext4	defaults	0 0
```



| 字段 | 内容         | 说明                                                         |
| :--- | :----------- | :----------------------------------------------------------- |
| 1    | 设备名       | 传统上，这个字段包含与物理设备相关联的设备文件的实际名字，比如说/dev/hda1（第一个 IDE 通道上第一个主设备分区）。然而今天的计算机，有很多热插拔设备（像 USB 驱动设备），许多 现代的 Linux 发行版用一个文本标签和设备相关联。当这个设备连接到系统中时， 这个标签（当储存媒介格式化时，这个标签会被添加到存储媒介中）会被操作系统读取。 那样的话，不管赋给实际物理设备哪个设备文件，这个设备仍然能被系统正确地识别。 |
| 2    | 挂载点       | 设备所连接到的文件系统树的目录。                             |
| 3    | 文件系统类型 | Linux 允许挂载许多文件系统类型。大多数本地的 Linux 文件系统是 ext3， 但是也支持很多其它的，比方说 FAT16 (msdos), FAT32 (vfat)，NTFS (ntfs)，CD-ROM (iso9660)，等等。 |
| 4    | 选项         | 文件系统可以通过各种各样的选项来挂载。有可能，例如，挂载只读的文件系统， 或者挂载阻止执行任何程序的文件系统（一个有用的安全特性，避免删除媒介。） |
| 5    | 频率         | 一位数字，指定是否和在什么时间用 dump 命令来备份一个文件系统。 |
| 6    | 次序         | 一位数字，指定 fsck 命令按照什么次序来检查文件系统。         |



#### 查看挂载的文件系统列表

这个 mount 命令被用来挂载文件系统。执行这个不带参数的命令，将会显示 一系列当前挂载的文件系统：

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw,noexec,nosuid,nodev)
sysfs on /sys type sysfs (rw,noexec,nosuid,nodev)
none on /sys/fs/cgroup type tmpfs (rw)
none on /sys/fs/fuse/connections type fusectl (rw)
none on /sys/kernel/debug type debugfs (rw)
none on /sys/kernel/security type securityfs (rw)
udev on /dev type devtmpfs (rw,mode=0755)
devpts on /dev/pts type devpts (rw,noexec,nosuid,gid=5,mode=0620)
tmpfs on /run type tmpfs (rw,noexec,nosuid,size=10%,mode=0755)
none on /run/lock type tmpfs (rw,noexec,nosuid,nodev,size=5242880)
none on /run/shm type tmpfs (rw,nosuid,nodev)
none on /run/user type tmpfs (rw,noexec,nosuid,nodev,size=104857600,mode=0755)
none on /sys/fs/pstore type pstore (rw)
rpc_pipefs on /run/rpc_pipefs type rpc_pipefs (rw)
systemd on /sys/fs/cgroup/systemd type cgroup (rw,noexec,nosuid,nodev,none,name=systemd)
vagrant on /vagrant type vboxsf (uid=1000,gid=1000,rw)
```

我们不能卸载一个设备，如果某个用户或进程正在使用这个设备的话。在这种 情况下，我们把工作目录更改到了 CD-ROW 的挂载点，这个挂载点导致设备忙碌。我们可以很容易地修复这个问题 通过把工作目录改到其它目录而不是这个挂载点。

```shell
[root@linuxbox cdrom]## cd
[root@linuxbox ~]## umount /dev/hdc
```



 *Linux 存储设备名称*

```shell
[me@linuxbox ~]$ ls /dev
```



| 模式     | 设备                                                         |
| :------- | :----------------------------------------------------------- |
| /dev/fd* | 软盘驱动器                                                   |
| /dev/hd* | 老系统中的 IDE(PATA)磁盘。典型的主板包含两个 IDE 连接器或者是通道，每个连接器 带有一根缆线，每根缆线上有两个硬盘驱动器连接点。缆线上的第一个驱动器叫做主设备， 第二个叫做从设备。设备名称这样安排，/dev/hda 是指第一通道上的主设备名；/dev/hdb 是第一通道上的从设备名；/dev/hdc 是第二通道上的主设备名，等等。末尾的数字表示 硬盘驱动器上的分区。例如，/dev/hda1是指系统中第一硬盘驱动器上的第一个分区，而 /dev/hda 则是指整个硬盘驱动器。 |
| /dev/lp* | 打印机                                                       |
| /dev/sd* | SCSI 磁盘。在最近的 Linux 系统中，内核把所有类似于磁盘的设备（包括 PATA/SATA 硬盘， 闪存，和 USB 存储设备，比如说可移动的音乐播放器和数码相机）看作 SCSI 磁盘。 剩下的命名系统类似于上述所描述的旧的/dev/hd*命名方案。 |
| /dev/sr* | 光盘（CD/DVD 读取器和烧写器）                                |

## 网络系统

当谈及到网络系统层面，几乎任何东西都能由 Linux 来实现。Linux 被用来创建各式各样的网络系统和装置， 包括防火墙，路由器，名称服务器，网络连接式存储设备等等。

```shell
ping - 发送 ICMP ECHO_REQUEST 数据包到网络主机

traceroute - 打印到一台网络主机的路由数据包

netstat - 打印网络连接，路由表，接口统计数据，伪装连接，和多路广播成员

ftp - 因特网文件传输程序

wget - 非交互式网络下载器

ssh - OpenSSH SSH 客户端（远程登录程序）
```

#### 检查和监测网络

##### ping

最基本的网络命令是 ping。这个 ping 命令发送一个特殊的网络数据包，叫做 ICMP ECHO_REQUEST，到 一台指定的主机。大多数接收这个包的网络设备将会回复它，来允许网络连接验证。

注意：大多数网络设备（包括 Linux 主机）都可以被配置为忽略这些数据包。通常，这样做是出于网络安全 原因，部分地遮蔽一台主机免受一个潜在攻击者地侵袭。配置防火墙来阻塞 IMCP 流量也很普遍。

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ ping -c3 www.baidu.com
PING www.a.shifen.com (180.101.49.12) 56(84) bytes of data.
64 bytes from 180.101.49.12: icmp_seq=1 ttl=63 time=16.5 ms
64 bytes from 180.101.49.12: icmp_seq=2 ttl=63 time=16.4 ms
64 bytes from 180.101.49.12: icmp_seq=3 ttl=63 time=16.3 ms

--- www.a.shifen.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 16.392/16.475/16.543/0.160 ms
```

按下组合键 Ctrl-c，中断这个命令之后，ping 打印出运行统计信息。一个正常工作的网络会报告 零个数据包丢失。一个成功执行的“ping”命令会意味着网络的各个部件（网卡，电缆，路由，网关） 都处于正常的工作状态。

##### traceroute

这个 traceroute 程序（一些系统使用相似的 tracepath 程序来代替）会显示从本地到指定主机 要经过的所有“跳数”的网络流量列表。例如，看一下到达 baidu.com 需要经过的路由， 我们将这样做：

```shell
traceroute to www.baidu.com (180.101.49.12), 30 hops max, 60 byte packets
 1  10.0.2.2 (10.0.2.2)  0.116 ms  0.101 ms  0.265 ms
 2  192.168.31.1 (192.168.31.1)  1.573 ms  1.615 ms  1.738 ms
 3  192.168.1.1 (192.168.1.1)  2.199 ms  2.179 ms  2.162 ms
 4  115.198.100.1 (115.198.100.1)  4.624 ms  4.870 ms  4.742 ms
 5  61.164.24.56 (61.164.24.56)  5.160 ms 61.164.24.54 (61.164.24.54)  5.151 ms 61.164.24.124 (61.164.24.124)  5.749 ms
 6  220.191.198.153 (220.191.198.153)  5.686 ms 220.191.143.176 (220.191.143.176)  10.609 ms 61.164.8.118 (61.164.8.118)  20.272 ms
 7  202.97.33.157 (202.97.33.157)  15.552 ms 202.97.33.145 (202.97.33.145)  14.209 ms 202.97.100.165 (202.97.100.165)  14.515 ms
 8  58.213.94.110 (58.213.94.110)  10.604 ms 58.213.94.2 (58.213.94.2)  13.770 ms 58.213.95.114 (58.213.95.114)  15.166 ms
 9  * * *
10  58.213.96.74 (58.213.96.74)  17.679 ms 58.213.96.58 (58.213.96.58)  16.258 ms 58.213.96.106 (58.213.96.106)  18.236 ms
11  * * *
12  * * *
13  * * *
```



从输出结果中，我们可以看到连接测试系统到 slashdot.org 网站需要经由16个路由器。对于那些 提供标识信息的路由器，我们能看到它们的主机名，IP 地址和性能数据，这些数据包括三次从本地到 此路由器的往返时间样本。对于那些没有提供标识信息的路由器（由于路由器配置，网络拥塞，防火墙等 方面的原因），我们会看到几个星号，正如行中所示。

##### mtr

组合了ping和traceroute的功能，mtr允许你不停地询问远程主机来查看延迟和性能变化

![image-20200424111645282](https://raw.githubusercontent.com/geekzsp/ImagesRepository/master/007S8ZIlly1ge4os04omgj31960m0dsx.jpg)

##### netstat

netstat 程序被用来检查各种各样的网络设置和统计数据。通过此命令的许多选项，我们 可以看看网络设置中的各种特性。使用“-ie”选项，我们能够查看系统中的网络接口：

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ netstat -ie
Kernel Interface table
eth0      Link encap:Ethernet  HWaddr 08:00:27:5f:bb:e6
          inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fe5f:bbe6/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9423 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6524 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:827098 (827.0 KB)  TX bytes:669793 (669.7 KB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

在上述实例中，我们看到我们的测试系统有两个网络接口。第一个，叫做 eth0，是 以太网接口，和第二个，叫做 lo，是内部回环网络接口，它是一个虚拟接口，系统用它来 “自言自语”。

当执行日常网络诊断时，要查看的重要信息是每个网络接口第四行开头出现的单词 **“UP”**，说明这个网络接口已经生效，还要查看第二行中 inet addr 字段出现的有效 IP 地址。对于使用 DHCP（动态主机配置协议）的系统，在 这个字段中的一个有效 IP 地址则证明了 DHCP 工作正常。

使用这个“-r”选项会显示内核的网络路由表。这展示了系统是如何配置网络之间发送数据包的。

```shell
[me@linuxbox ~]$ netstat -r
Kernel IP routing table
Destination     Gateway     Genmask         Flags    MSS  Window  irtt Iface

192.168.1.0     *           255.255.255.0   U        0    0          0 eth0
default         192.168.1.1 0.0.0.0         UG       0    0          0 eth0
```

在这个简单的例子里面，我们看到了，位于防火墙之内的局域网中，一台客户端计算机的典型路由表。 第一行显示了目的地 192.168.1.0。IP 地址以零结尾是指网络，而不是独立主机， 所以这个目的地意味着局域网中的任何一台主机。下一个字段，Gateway， 是网关（路由器）的名字或 IP 地址，用它来连接当前的主机和目的地的网络。 若这个字段显示一个星号，则表明不需要网关。

最后一行包含目的地 default。指的是发往任何表上没有列出的目的地网络的流量。 在我们的实例中，我们看到网关被定义为地址 192.168.1.1 的路由器，它应该能 知道怎样来处理目的地流量。

#### 网络中传输文件

#### ftp

#### wget

#### 与远程主机安全通信

##### ssh

为了解决这个问题，开发了一款新的协议，叫做 SSH（Secure Shell）。 SSH 解决了这两个基本的和远端主机安全交流的问题。首先，它要认证远端主机是否为它 所知道的那台主机（这样就阻止了所谓的“中间人”的攻击），其次，它加密了本地与远程主机之间 所有的通讯信息。

SSH 由两部分组成。SSH 服务端运行在远端主机上，在端口 22 上监听收到的外部连接，而 SSH 客户端用在本地系统中，用来和远端服务器通信。

大多数 Linux 发行版自带一个提供 SSH 功能的软件包，叫做 OpenSSH，来自于 BSD 项目。一些发行版 默认包含客户端和服务端两个软件包（例如 Red Hat），而另一些（比方说 Ubuntu）则只提供客户端。 为了能让系统接受远端的连接，它必须安装 OpenSSH-server 软件包，配置，运行它， 并且（如果系统正在运行，或者系统在防火墙之后）它必须允许在 TCP 端口 22 上接收网络连接。

```shell
$ ssh vagrant@127.0.0.1 -p 2222 free
The authenticity of host '[127.0.0.1]:2222 ([127.0.0.1]:2222)' can't be established.
ECDSA key fingerprint is SHA256:2ReK1BFFFmbLyn+1Pol9kq0ERuor4ZYPwKXZCMN/S1w.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```



第一次尝试连接，提示信息表明远端主机的真实性不能确立。这是因为客户端程序以前从没有 看到过这个远端主机。为了接受远端主机的身份验证凭据，输入“yes”。一旦建立了连接，会提示 用户输入他或她的密码：



```shell
[me@linuxbox ~]$ ssh remote-sys
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle
attack)!
...
```

有两种可能的情形会提示这些信息。第一，某个攻击者企图制造“中间人”袭击。这很少见， 因为每个人都知道 ssh 会针对这种状况发出警告。最有可能的罪魁祸首是远端系统已经改变了； 例如，它的操作系统或者是 SSH 服务器重新安装了。然而，为了安全起见，第一个可能性不应该 被轻易否定。当这条消息出现时，总要与远端系统的管理员查对一下。

当确定了这条消息归结为一个良性的原因之后，那么在客户端更正问题就很安全了。 使用文本编辑器（可能是 vim）从文件~/.ssh/known_hosts 中删除废弃的钥匙， 就解决了问题。



除了能够在远端系统中打开一个 shell 会话，ssh 程序也允许我们在远端系统中执行单个命令。 例如，在名为 remote-sys 的远端主机上，执行 free 命令，并把输出结果显示到本地系统 shell 会话中。

```shell
$ ssh vagrant@127.0.0.1 -p 2222 free
vagrant@127.0.0.1's password:
             total       used       free     shared    buffers     cached
Mem:        501576     405936      95640        368      20636     258900
-/+ buffers/cache:     126400     375176
Swap:            0          0          0
```



```shell
[me@linuxbox ~]$ ssh remote-sys 'ls \*' > dirlist.txt
me@twin4's password:
[me@linuxbox ~]
```

注意，上面的例子中使用了单引号。这样做是因为我们不想路径名展开操作在本地执行，而希望 它在远端系统中被执行。同样地，如果我们想要把输出结果重定向到远端主机的文件中，我们可以 把重定向操作符和文件名都放到单引号里面。

```
[me@linuxbox ~]$ ssh remote-sys 'ls * > dirlist.txt'
```



**SSH 通道**

当你通过 SSH 协议与远端主机建立连接的时候，其中发生的事就是在本地与远端系统之间 创建了一条加密通道。通常，这条通道被用来把在本地系统中输入的命令安全地传输到远端系统， 同样地，再把执行结果安全地发送回来。除了这个基本功能之外，SSH 协议允许大多数 网络流量类型通过这条加密通道来被传送，在本地与远端系统之间创建一种 VPN（虚拟专用网络）。

```shel
ssh -C -f -N -g -L listen_port:DST_Host:DST_port user@Tunnel_Host      
ssh -C -f -N -g -R listen_port:DST_Host:DST_port user@Tunnel_Host       
ssh -C -f -N -g -D listen_port user@Tunnel_Host
```

**scp 和 sftp**

OpenSSH 软件包也包含两个程序，它们可以利用 SSH 加密通道在网络间复制文件。 第一个，scp（安全复制）被用来复制文件，与熟悉的 cp 程序非常相似。最显著的区别就是 源或者目标路径名要以远端主机的名字，后跟一个冒号字符开头。例如，如果我们想要 从 remote-sys 远端系统的家目录下复制文档 document.txt，到我们本地系统的当前工作目录下， 可以这样操作：



#### 域名相关命令

##### nslookup

```shell
vagrant@vagrant-ubuntu-trusty-64:~$ nslookup www.taobao.com
Server:		10.0.2.3           --本机配置的域名服务器
Address:	10.0.2.3#53

Non-authoritative answer:
www.taobao.com	canonical name = www.taobao.com.danuoyi.tbcache.com.
Name:	www.taobao.com.danuoyi.tbcache.com
Address: 60.163.129.164
Name:	www.taobao.com.danuoyi.tbcache.com
Address: 60.163.129.165

```



#### dig

```shell
$ dig  www.baidu.com
; <<>> DiG 9.9.5-3ubuntu0.19-Ubuntu <<>> www.baidu.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60408
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;www.baidu.com.			IN	A

;; ANSWER SECTION:
www.baidu.com.		300	IN	CNAME	www.a.shifen.com.
www.a.shifen.com.	281	IN	A	180.101.49.12
www.a.shifen.com.	281	IN	A	180.101.49.11

;; Query time: 10 msec
;; SERVER: 10.0.2.3#53(10.0.2.3)   
;; WHEN: Fri Apr 24 06:56:53 UTC 2020
;; MSG SIZE  rcvd: 104
```

指定解析域名服务器

```
$ dig @223.5.5.5 www.baidu.com
```



域名解析路径跟踪

```shell
dig www.baidu.com +trace
```

## 归档和备份



### 压缩文件

纵观计算领域的发展历史，人们努力想把最多的数据存放到到最小的可用空间中，不管是内存，存储设备 还是网络带宽。今天我们把许多数据服务都看作是理所当然的事情，但是诸如便携式音乐播放器， 高清电视，或宽带网络之类的存在都应归功于高效的数据压缩技术。

压缩算法（数学技巧被用来执行压缩任务）分为两大类，无损压缩和有损压缩。无损压缩保留了 原始文件的所有数据。这意味着，当还原一个压缩文件的时候，还原的文件与原文件一模一样。 而另一方面，有损压缩，执行压缩操作时会删除数据，允许更大的压缩。当一个有损文件被还原的时候， 它与原文件不相匹配; 相反，它是一个近似值。有损压缩的例子有 JPEG（图像）文件和 MP3（音频）文件。

#### gzip

这个 gzip 程序被用来压缩一个或多个文件。当执行 gzip 命令时，则原始文件的压缩版会替代原始文件。 相对应的 gunzip 程序被用来把压缩文件复原为没有被压缩的版本。zip不能压缩整个文件夹 通常使用 带z参数的tar命令 来替代

```shell
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ ls
a.txt
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ gzip a.txt
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ ls
a.txt.gz
## 解压 gunzip 或者 gzip -d
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ gunzip a.txt.gz
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ ls
a.txt
```

| 选项    | 说明                                                         |
| :------ | :----------------------------------------------------------- |
| -c      | 把输出写入到标准输出，并且保留原始文件。也有可能用--stdout 和--to-stdout 选项来指定。 |
| -d      | 解压缩。正如 gunzip 命令一样。也可以用--decompress 或者--uncompress 选项来指定. |
| -f      | 强制压缩，即使原始文件的压缩文件已经存在了，也要执行。也可以用--force 选项来指定。 |
| -h      | 显示用法信息。也可用--help 选项来指定。                      |
| -l      | 列出每个被压缩文件的压缩数据。也可用--list 选项。            |
| -r      | 若命令的一个或多个参数是目录，则递归地压缩目录中的文件。也可用--recursive 选项来指定。 |
| -t      | 测试压缩文件的完整性。也可用--test 选项来指定。              |
| -v      | 显示压缩过程中的信息。也可用--verbose 选项来指定。           |
| -number | 设置压缩指数。number 是一个在1（最快，最小压缩）到9（最慢，最大压缩）之间的整数。 数值1和9也可以各自用--fast 和--best 选项来表示。默认值是整数6。 |

### 归档文件

一个常见的，与文件压缩结合一块使用的文件管理任务是归档。归档就是收集许多文件，并把它们 捆绑成一个大文件的过程。归档经常作为系统备份的一部分来使用。当把旧数据从一个系统移到某 种类型的长期存储设备中时，也会用到归档程序。

#### tar

在类 Unix 的软件世界中，这个 tar 程序是用来归档文件的经典工具。它的名字，是 tape archive 的简称，揭示了它的根源，它是一款制作磁带备份的工具。而它仍然被用来完成传统任务， 它也同样适用于其它的存储设备。我们经常看到扩展名为 .tar 或者 .tgz 的文件，它们各自表示“普通” 的 tar 包和被 gzip 程序压缩过的 tar 包。一个 tar 包可以由一组独立的文件，一个或者多个目录，或者 两者混合体组成。命令语法如下：

```shell
## 压缩  zcvf  -z或--gzip或--ungzip：通过gzip指令压缩/解压缩文件，文件名最好为*.tar.gz；
[me@linuxbox foo]$ tar cf playground.tar playground
## 解压  zxvf
[me@linuxbox foo]$ tar xf ../playground2.tar
```

| 模式 | 说明                               |
| :--- | :--------------------------------- |
| c    | 为文件和／或目录列表创建归档文件。 |
| x    | 抽取归档文件。                     |
| r    | 追加具体的路径到归档文件的末尾。   |
| t    | 列出归档文件的内容。               |

#### zip

这个 zip 程序既是压缩工具，也是一个打包工具。这程序使用的文件格式，Windows 用户比较熟悉， 因为它读取和写入.zip 文件。然而，在 Linux 中 gzip 是主要的压缩程序，而 bzip2则位居第二。

```shell
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ zip test.zip b.txt
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ unzip test.zip
```

[Linux下常用压缩 解压命令和压缩比率对比](https://www.cnblogs.com/joshua317/p/6170839.html)

对比bzip2(.bz2)、gzip(.gz)、zip(.zip)来看，**压缩率：bzip2>gzip>zip。**

一般我们打包文件多为网站文件（即txt），推荐使用tar+gzip的方式来进行打包 推荐使用 tar.gz(tgz)。

虽然zip是通用性最好的格式，但是现在windows平台下各解压缩软件对gzip格式的支持也是越来越好了。而bz2所占用的CPU时间比其他两种格式要长，所以综合考虑gzip目前是最佳选择。

### 同步文件和目录

维护系统备份的常见策略是保持一个或多个目录与另一个本地系统（通常是某种可移动的存储设备） 或者远端系统中的目录（或多个目录）同步。我们可能，例如有一个正在开发的网站的本地备份， 需要时不时的与远端网络服务器中的文件备份保持同步。在类 Unix 系统的世界里，能完成此任务且 备受人们喜爱的工具是 rsync。这个程序能同步本地与远端的目录，通过使用 rsync 远端更新协议，此协议 允许 rsync 快速地检测两个目录的差异，执行最小量的复制来达到目录间的同步。比起其它种类的复制程序， 这就使 rsync 命令非常快速和高效。

rsync 中的“r”象征着“remote”

```shell
rsync options source destination
```

注意 source 和 destination 两者之一必须是本地文件。rsync 不支持远端到远端的复制

```shell
-v, --verbose 详细模式输出。
-a, --archive 归档模式，表示以递归方式传输文件，并保持所有文件属性，等于-rlptgoD。
-z, --compress 对备份的文件在传输时进行压缩处理。
```

```shell
vagrant@vagrant-ubuntu-trusty-64:~/ziptest$ rsync -av a.txt b.txt
sending incremental file list
a.txt

sent 105 bytes  received 35 bytes  280.00 bytes/sec
total size is 0  speedup is 0.00
```



在这个例子里，我们把/etc，/home，和/usr/local 目录从我们的系统中复制到假想的存储设备中。 我们包含了–delete 这个选项，来删除可能在备份设备中已经存在但却不再存在于源设备中的文件， （这与我们第一次创建备份无关，但是会在随后的复制操作中有用途）。挂载外部驱动器，运行 rsync 命令，不断重复这个过程，是一个不错的（虽然不理想）方式来保存少量的系统备份文件。 当然，别名会对这个操作更有帮助些。我们将会创建一个别名，并把它添加到.bashrc 文件中， 来提供这个特性：

```shell
alias backup='sudo rsync -av --delete /etc /home /usr/local /media/BigDisk/backup'
```



rsync 可以被用来在网络间同步文件的第二种方式是通过使用 rsync 服务器。rsync 可以被配置为一个 守护进程，监听即将到来的同步请求。这样做经常是为了进行一个远程系统的镜像操作。例如，Red Hat 软件中心为它的 Fedora 发行版，维护着一个巨大的正在开发中的软件包的仓库。对于软件测试人员， 在发行周期的测试阶段，定期镜像这些软件集合是非常有帮助的。因为仓库中的这些文件会频繁地 （通常每天不止一次）改动，定期同步本地镜像而不是大量地拷贝软件仓库，这是更为明智的。 这些软件库之一被维护在乔治亚理工大学；我们可以使用本地 rsync 程序和它们的 rsync 服务器来镜像它。

```shell
[me@linuxbox ~]$ mkdir fedora-devel
[me@linuxbox ~]$ rsync -av -delete rsync://rsync.gtlib.gatech.edu/fedora-linux-
 core/development/i386/os fedora-devel
```



## select poll epoll的区别  IO多路复用模型

在linux没有实现epoll事件驱动机制之前，我们一般选择用select或者poll等IO多路复用的方法来实现并发服务程序。在大数据、高并发、集群等一些名词唱的火热之年代，select和poll的用武之地越来越有限了，风头已经被epoll占尽。



**select的缺点：**

单个进程能够监视的文件描述符的数量存在最大限制，通常是1024，当然可以更改数量，但由于select采用轮询的方式扫描文件描述符，文件描述符数量越多，性能越差；

内核/用户空间内存拷贝问题，select需要复制大量的句柄数据结构，产生巨大的开销；

select返回的是含有整个句柄的***数组\***，应用程序需要遍历整个数组才能发现哪些句柄发生了事件；

select的触发方式是水平触发，应用程序如果没有完成对一个已经就绪的文件描述符进行IO，那么之后再次select调用还是会将这些文件描述符通知进程。



**poll的缺点:**

相比于select模型，poll使用***链表\***保存文件描述符，因此没有了监视文件数量的限制，但其他三个缺点依然存在。



拿select模型为例，假设我们的服务器需要支持100万的并发连接，则在_FD_SETSIZE为1024的情况下，则我们至少需要开辟1k个进程才能实现100万的并发连接。除了进程间上下文切换的时间消耗外，从内核/用户空间大量的无脑内存拷贝、数组轮询等，是系统难以承受的。因此，基于select模型的服务器程序，要达到10万级别的并发访问，是一个很难完成的任务。



epoll的设计和实现select完全不同。epoll通过在linux内核中申请一个简易的文件系统（文件系统一般用什么数据结构实现？B+树）。把原先的select/poll调用分成了3个部分：

1）调用epoll_create()建立一个epoll对象（在epoll文件系统中为这个句柄对象分配资源）

2）调用epoll_ctl向epoll对象中添加这100万个连接的套接字

3）调用epoll_wait收集发生的事件的连接







select，poll，epoll都是IO多路复用的机制。I/O多路复用就是通过一种机制，一个进程可以监视多个描述符，一旦某个描述符就绪（一般是读就绪或者写就绪），能够通知程序进行相应的读写操作。但select，poll，epoll本质上都是同步I/O，因为他们都需要在读写事件就绪后自己负责进行读写，也就是说这个读写过程是阻塞的，而异步I/O则无需自己负责进行读写，异步I/O的实现会负责把数据从内核拷贝到用户空间。（这里啰嗦下）







####### 红黑树 和 b+树的用途有什么区别？

1. 红黑树多用在内部排序，即全放在内存中的，STL的map和set的内部实现就是红黑树。
2. B+树多用于外存上时，B+也被成为一个磁盘友好的数据结构。

**为什么b+磁盘友好？**

1. 磁盘读写代价更低
    树的非叶子结点里面没有数据，这样索引比较小，可以放在一个blcok（或者尽可能少的blcok）里面。避免了树形结构不断的向下查找，然后磁盘不停的寻道，读数据。这样的设计，可以降低io的次数。
2. 查询效率更加稳定
    非终结点并不是最终指向文件内容的结点，而只是叶子结点中关键字的索引。所以任何关键字的查找必须走一条从根结点到叶子结点的路。所有关键字查询的路径长度相同，导致每一个数据的查询效率相当。
3. 遍历所有的数据更方便
    B+树只要遍历叶子节点就可以实现整棵树的遍历，而其他的树形结构 要中序遍历才可以访问所有的数据。







## 常用命令

#### 1.系统指标相关

top free lsof ps -aux  kill shotdown

#### 2.网络相关

telnet ifconfig dig ping  traceroute mtr curl wget  ssh netstat df

#### 3.文件相关

Chmod Chown touch vim  tar zip  gzip   mkdir cd  rm  rmdir  mv cp  ls    du ln find     witch whereis type

#### 4.文本相关

tail head more less

