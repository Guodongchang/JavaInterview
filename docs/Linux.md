# Linux

Linux

## 操作技巧

在 Linux 里面Vim操作任何文件，都提前拷贝一份，这是好习惯。

```
cp application.properties application.properties.init
```



# Linux简介

# Linux文件系统概览

## Linux文件系统简介

**在Linux操作系统中，所有被操作系统管理的资源，例如网络接口卡、磁盘驱动器、打印机、输入输出设备、普通文件或是目录都被看作是一个文件。**

也就是说在LINUX系统中有一个重要的概念：**一切都是文件**。其实这是UNIX哲学的一个体现，而Linux是重写UNIX而来，所以这个概念也就传承了下来。在UNIX系统中，把一切资源都看作是文件，包括硬件设备。UNIX系统把每个硬件都看成是一个文件，通常称为设备文件，这样用户就可以用读写文件的方式实现对硬件的访问。

## Inode

inode是linux/unix文件系统和硬盘存储的基础，如果理解了inode，
将会对我们学习如何将复杂的概念抽象成简单概念有重大帮助。

### Inode是什么?有什么作用?

文件存储在硬盘上，硬盘的最小存储单位是扇区(Sector),每个扇区存储512字节(0.5kb)。
操作系统读取硬盘的数据时，不会一个扇区一个扇区的读取，这样做效率较低，而是**一次读取多个扇区，
即一次读取一个块(block)。块由多个扇区组成，是文件读取的最小单位，块的最常见的大小是4kb，
约为8个连续的扇区组成。文件数据存储在块中，**
但还需要一个空间来存储文件的元信息metadata，如文件拥有者，创建时间，权限，大小等。
这种**存储文件元信息的区域就叫inode，译为索引节点。 每个文件都有一个inode，存储文件的元信息。
使用 stat 命令可以查看文件的inode信息。每个inode都有一个号码，
Linux/Unix操作系统不使用文件名来区分文件，而是使用inode号码区分不同的文件。**

**inode也需要消耗硬盘空间，所以在格式化硬盘的时候，操作系统会将硬盘分为2个区域，
一个区域存放文件数据，另一个区域存放inode所包含的信息，
存放inode的区域被称为inode table。**

文件的inode信息:

![文件inode信息](../media/pictures/Linux.assets/%E6%96%87%E4%BB%B6inode%E4%BF%A1%E6%81%AF.png)

## 文件类型与目录结构

**Linux支持很多文件类型，其中非常重要的文件类型有: 
普通文件，目录文件，链接文件，设备文件，管道文件，Socket套接字文件等。

![文件类型](../media/pictures/Linux.assets/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f332f313634356631613764363464656631613f773d39303126683d35343726663d706e6726733d3732363932.jpg)

- 普通文件: 普通文件是指txt,html,pdf等等的这样应用层面的文件类型，
  用户可以根据访问权限对普通文件进行访问，修改和删除。
- 目录文件: 目录也是一种文件，打开目录实际上是打开目录文件。
  目录文件包含了它目录下的所有文件名以及指向这些文件的指针。

![目录文件](../media/pictures/Linux.assets/%E7%9B%AE%E5%BD%95%E6%96%87%E4%BB%B6.png)

- 链接文件: 链接文件分为符号链接(软链接)文件和硬链接文件
  - 硬链接(Hard Link):硬链接的文件拥有相同的inode，因为操作系统是靠inode来区分文件的，
    2个inode相同的文件，就代表它们是一个文件。
    删除一个文件并不会对其他拥有相同inode的文件产生影响，只有当inode相同的所有文件被删除了，
    这个文件才会被删除。换言之，你建立一个文件的硬链接，这个文件和硬链接它们的inode是相同的,
    无论你删除的是硬链接还是源文件，都不会对彼此造成影响,除非你把硬链接和源文件都删除，
    这个文件才被删除。
  - 符号链接(软链接)(Symbolic Link): 符号链接类似于Windows上的快捷方式，它保存了源文件的路径。
    当符号链接被删除时，并不会影响源文件。但是当源文件被删除时，符号链接就找不到源文件了。

软链接和硬链接:

![软链接和硬链接](../media/pictures/Linux.assets/%E8%BD%AF%E9%93%BE%E6%8E%A5%E5%92%8C%E7%A1%AC%E9%93%BE%E6%8E%A5.png)

- 设备文件
  设备文件分为块设备文件和字符设备文件,设备文件一般存于/dev目录下。
  - 字符设备文件: **字符设备是依照先后顺序被存取数据的设备，通常不支持随机存取，
    此类设备可以按字节/字符来读取数据，** 如键盘，串口等等。
  - 块设备文件: **块设备是可以被随机存取数据的设备，应用程序可以访问块设备上任何一块位置。
    块设备以块的方式读取数据，在windows下也称为簇，块设备不支持字符的方式寻址。**
    如硬盘，软盘，光碟等等。

**字符设备与块设备最根本的区别就是它们是否可以被随机访问。**
如键盘，当我们在键盘上敲下一个单词: "word"的时候，
那么系统肯定是需要按照顺序来进行读取word的字节流(字符流)的，随机访问在此时是没有意义的。

- 管道文件: 管道文件一般用于进程间通信，使用mkfifo命令可以创建一个管道文件。
- Socket套接字文件: 套接字文件被用于网络进程之间的通信，既可以使2台不同的机器进行通信，也可以用于本机的Socket网络程序。

## Linux文件系统目录

![](../media/pictures/Linux.assets/2aba35eefe49f539412c5a65a993249e.png)



- **/**：根目录，所有的目录、文件、设备都在/之下，/就是Linux文件系统的组织者，也是最上级的领导者。
- **/bin**：就是二进制（binary）英文缩写。在一般的系统当中，都可以在这个目录下找到linux常用的命令。系统所需要的那些命令位于此目录。
- **/boot**：Linux的内核及引导系统程序所需要的文件目录。
- **/dev**：是设备（device)的英文缩写。这个目录对所有的用户都十分重要。因为在这个目录中包含了所有linux系统中使用的外部设备。但是这里并不是放的外部设备的驱动程序。这一点和常用的windows,dos操作系统不一样。它实际上是一个访问这些外部设备的端口。可以非常方便地去访问这些外部设备，和访问一个文件，一个目录没有任何区别。
- **/home**：如果建立一个用户，用户名是"xx",那么在/home目录下就有一个对应的/home/xx路径，用来存放用户的主目录。家目录
- **/lib**：是库（library）英文缩写。这个目录是用来存放系统动态连接共享库的。几乎所有的应用程序都会用到这个目录下的共享库。因此，千万不要轻易对这个目录进行什么操作，一旦发生问题，系统就不能工作了；
- **/proc**：虚拟文件系统目录，是系统内存的映射。可直接访问这个目录来获取系统信息；
- **/root**：Linux超级权限用户root的家目录；
- **/sbin**：这个目录是用来存放系统管理员的系统管理程序。大多是涉及系统管理的命令的存放，是超级权限用户root的可执行命令存放地，普通用户无权限执行这个目录下的命令，sbin中包含的都是root权限才能执行的；
- **/usr**： 用于存放系统应用程序，这是linux系统中占用硬盘空间最大的目录。用户的很多应用程序和文件都存放在这个目录下。Unix software resource usr。
- **/usr/local**：这里主要存放那些手动安装的软件，即不是通过或apt-get安装的软件。它和/usr目录具有相类似的目录结构。
- **/usr/share** ：系统共用的东西存放地，比如 /usr/share/fonts是字体目录，/usr/share/do和/usr/share/man帮助文件。
- **/etc**：  存放系统管理和配置文件；
- **/opt：** 额外安装的可选应用程序包所放置的位置。一般情况下，我们可以把tomcat等都安装到这里
- **/mnt：** 系统管理员安装临时文件系统的安装点，系统提供这个目录是让用户临时挂载其他的文件系统；
- **/tmp：** 用于存放各种临时文件，是公用的临时文件存储点；
- **/var：** 用于存放运行时需要改变数据的文件，也是某些大文件的溢出区，比方说各种服务的日志文件（系统启动日志等。）等；
- **/lost+found：**  这个目录平时是空的，系统非正常关机而留下“无家可归”的文件（windows下叫什么.chk）就在这里。



## Linux中# 和 $ 的区别：

【#】代表 root权限
【$】代表普通用户

 

如果更改了/etc/profile , 或~/.bashrc等文档，可以用任何符号来代替它们。

linux窗口下的【root@locate~】其中的【~】代表代表用户的家目录（root为/root，一般user则为/home/username）；【./】和【.】代表当前目录；【../】代表上级目录



# Linux 命令

命令大全：https://man.linuxde.net/



## 进入超级用户 su root

## cd 目录切换命令

- **`cd usr`：**   切换到该目录下usr目录  
- **`cd ..（或cd../）`：**  切换到上一层目录 
- **`cd /`：**   切换到系统根目录  
- **`cd ~`：**   切换到用户主目录 
- **`cd -`：**   切换到上一个操作所在目录

**善于使用tab健 去补全路径的名称。**

## 目录的操作命令(增删改查)

- **`mkdir 目录名称`：** 增加目录

  - -p或--parents 若所要建立目录的上层目录目前尚未建立，则会一并建立上层目录；
  - --version 显示版本信息。

- **`ls或者ll`**（ll是ls -l的别名，ll命令可以看到该目录下的所有目录和文件的详细信息）：查看目录信息

  - ls ：查看目标目录下的文件或目录名称（不包括隐藏文件）
  - ls -a：查看目标目录下的文件或目录的名称（包括隐藏文件）
  - ls -l：查看目标目录下的文件或名称的详细信息
  - ll 会列出该文件下的所有文件信息，包括隐藏的文件
  - ll -h 友好的显示

- **`find 目录 参数`：** 寻找目录（查）

  示例：

  - 列出当前目录及子目录下所有文件和文件夹: `find .`
  - 在`/home`目录下查找以.txt结尾的文件名:`find /home -name "*.txt"`
  - 同上，但忽略大小写: `find /home -iname "*.txt"`
  - 当前目录及子目录下查找所有以.txt和.pdf结尾的文件:`find . \( -name "*.txt" -o -name "*.pdf" \)`或`find . -name "*.txt" -o -name "*.pdf" `

- **`mv 目录名称 新目录名称`：** 修改目录的名称（改）

  注意：mv的语法不仅可以对目录进行重命名而且也可以对各种文件，压缩包等进行  重命名的操作。mv命令用来对文件或目录重新命名，或者将文件从一个目录移到另一个目录中。后面会介绍到mv命令的另一个用法。

- **`mv 目录名称 目录的新位置`：**  移动目录的位置---剪切（改）

  注意：mv语法不仅可以对目录进行剪切操作，对文件和压缩包等都可执行剪切操作。另外mv与cp的结果不同，mv好像文件“搬家”，文件个数并未增加。而cp对文件进行复制，文件个数增加了。

- **`cp -r 目录名称 目录拷贝的目标位置`：** 拷贝目录（改），-r代表递归拷贝 

  注意：cp命令不仅可以拷贝目录还可以拷贝文件，压缩包等，拷贝文件和压缩包时不  用写-r递归

- **`rm [-rf] 目录`:** 删除目录（删）

  注意：rm不仅可以删除目录，也可以删除其他文件或压缩包，为了增强大家的记忆，  无论删除任何目录或文件，都直接使用`rm -rf` 目录/文件/压缩包，如果不加`-rf`删除的只能是空目录。

  - -p或--parents：删除指定目录后，若该目录的上层目录已变成空目录，则将其一并删除；
  - 注意：子目录被删除之前应该是空目录。就是说，该目录中的所有文件必须用rm命令全部，另外，当前工作目录必须在被删除目录之上，不能是被删除目录本身，也不能是被删除目录的子目录。

- **`pwd`**：查看当前目录，通常配合ls (Print Working Directory)



## 文件的操作命令(增删改查)

- **`touch 文件名称`:**  文件的创建（增）

  - touch  1.log　2.log 一次建立了两个1和2 日志文件

  - touch  1.log 一次创建一个文件

  - \-c 文件不存在时不创建新文件，如果存在，就会更新时间，证明它被人动过

  - -t 使用指定时间更新作为指定文件相对时间戳记的新值.此处的time规定为如下形式的十进制数：[[CC]YY]MMDDhhmm[.SS]

    这里，CC为年数中的前两位，即“世纪数”；YY为年数的后两位，即某世纪中的年数。如果不给出CC的值，则touch将把年数CCYY限定在1969--2068之内，MM为月数，DD为天数，hh为小时数，mm为分钟数，SS为秒数。

- **`cat/more/less/tail/head 文件名称`** 文件的查看（查）

  - **`cat`：** 查看显示整个文件内容

  - **`more`：** 可以显示百分比，回车可以向下一行， 空格可以向下一页，q可以退出查看，显示一屏

    - 空格：下一屏

      Enter：下一行

      b：上一页

      q：退出

  - **`less`：** 可以使用键盘上的PgUp和PgDn向上 和向下翻页，q结束查看

  - **`tail-10` ：** 查看文件的后10行，Ctrl+C结束

    - tail –c 10 查看文件的最后10个字符
    - 其中，**tail -20f 文件名可动态查看文件
    - **Ctrl+c结束查看**

  - **`head`**：查看文件的前几行

  注意：命令 tail -f 文件 可以对某个文件进行动态监控，例如tomcat的日志文件，  会随着程序的运行，日志会变化，可以使用tail -f catalina-2016-11-11.log 监控 文 件的变化 

- **`vim 文件`：**  修改文件的内容（改）

  vim编辑器是Linux中的强大组件，是vi编辑器的加强版，vim编辑器的命令和快捷方式有很多，但此处不一一阐述，大家也无需研究的很透彻，使用vim编辑修改文件的方式基本会使用就可以了。

  **在实际开发中，使用vim编辑器主要作用就是修改配置文件，下面是一般步骤：**

   vim 文件------>进入文件----->命令模式------>按i进入编辑模式----->编辑文件  ------->按Esc进入底行模式----->输入：wq/q! （输入wq代表写入内容并退出，即保存；输入q!代表强制退出不保存。）

- **`rm -rf 文件`：** 删除文件（删）

  同目录删除：熟记 `rm -rf` 文件 即可

  - rm 在ubuntu中所带的默认参数是-f，即强制删除，若想要询问删除则加参数-i
  - 当删除的是目录时必须加参数 -rf，在ubuntu中-r即可
  - 不进入回收站 rm –rf /

- **`stat`** 用于显示文件的状态信息。stat命令的输出信息比[ls](http://man.linuxde.net/ls)命令的输出信息要更详细。

  - -L：支持符号连接；
  - -f：显示文件系统状态而非文件状态；
  - -t：以简洁方式输出信息；
  - --help：显示指令的帮助信息；
  - --version：显示指令的版本信息。

- **`cp `** 文件复制操作   cp application.properties application.properties.init 

  - 当source为目录（文件夹）时，必须加参数 -r 即 cp src目录 destination；
  - 当source 为目录时，同时destination中如果有同名目录，则需要加-f 或
    -i参数，ubuntu中默认为-f force

- **`mv`** source(目录或文件名) desc（目录或文件）移动或者重命名文件

  - 若desc是目录名称就只完成移动功能，否则，可以完成重命名的功能。



**如果要查看日志的话**：

```shell
less logs/log.log 查看日志 可以上下翻页
```

## 压缩文件的操作命令

**1）打包并压缩文件：**

Linux中的打包文件一般是以.tar结尾的，压缩的命令一般是以.gz结尾的。

而一般情况下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。
命令：**`tar -zcvf 打包压缩后的文件名 要打包压缩的文件`**
其中：

- -z：调用gzip压缩命令进行压缩
- -c：打包文件，创建一个tar文件
- -v：显示运行过程
- -f：指定文件名
- -t：查看压缩文件的内容
- -x：解开tar文件

比如：假如test目录下有三个文件分别是：aaa.txt bbb.txt ccc.txt，如果我们要打包test目录并指定压缩后的压缩包名称为test.tar.gz可以使用命令：**`tar -zcvf test.tar.gz aaa.txt bbb.txt ccc.txt`或：`tar -zcvf test.tar.gz       /test/`**

**2）解压压缩包：**

命令：tar [-xvf] 压缩文件

其中：x：代表解压

示例：

1 将/test下的test.tar.gz解压到当前目录下可以使用命令：**`tar -xvf test.tar.gz`**

2 将/test下的test.tar.gz解压到根目录/usr下:**`tar -xvf test.tar.gz -C /usr`**（- C代表指定解压的位置 大写）



## 查找命令

- **`grep`**: 查找内容  grep options pattern file
  - Pattern 即正则表达式，正则表达式要用 单或双引号括起来。
  - grep asdf 1.txt 查找以asdf开头的字符串，在文件1.txt中
  - grep a* 1.txt 查出来的 只有全是a的。比如：aaaaa
- **`|`** 管道命令  它能将经由前一个命令的标准输出，作为管道后一个命令的标准输入。
  - ps -aux | grep java  查找进程中带java的
- **`find 起始目录 查找条件`** 查找文件
  - -name 指明按照文件名查找（可使用正则） find -name "test" 查找出来都是test文件名
  - -empty 查找大小为0的文件或空目录  find -empty 查找空文件
  - -type 查找类型为指定类型的文件或目录（类型d代表目录，f代表普通文件）find -type f -name test
  - -user ‘xx’ 查找名为xx的用户的所有文件   find -type d -name test -user root
  - -maxdepth 限制文件查找的范围，即在几层子目录之内查找(maxdepth需要在前面) find -maxdepth 1 type d -name test 



## Linux的文件权限命令

 操作系统中每个文件都拥有特定的权限、所属用户和所属组。权限是操作系统用来限制资源访问的机制，在Linux中权限一般分为读(readable)、写(writable)和执行(excutable)，分为三组。分别对应文件的属主(owner)，属组(group)和其他用户(other)，通过这样的机制来限制哪些用户、哪些组可以对特定的文件进行什么样的操作。通过 **`ls -l`** 命令我们可以  查看某个目录下的文件或目录的权限

示例：在随意某个目录下`ls -l`

![](../media/pictures/Linux.assets/1646955be781daaa)

第一列的内容的信息解释如下：

![](../media/pictures/Linux.assets/16469565b6951791)

> 下面将详细讲解文件的类型、Linux中权限以及文件有所有者、所在组、其它组具体是什么？

**文件的类型：**

- d： 代表目录
- -： 代表文件
- l： 代表软链接（可以认为是window中的快捷方式）

**Linux中权限分为以下几种：**

- r：代表权限是可读，r也可以用数字4表示
- w：代表权限是可写，w也可以用数字2表示
- x：代表权限是可执行，x也可以用数字1表示

**文件和目录权限的区别：**

 对文件和目录而言，读写执行表示不同的意义。

 对于文件：

| 权限名称 |                可执行操作 |
| :------- | ------------------------: |
| r        | 可以使用cat查看文件的内容 |
| w        |        可以修改文件的内容 |
| x        |  可以将其运行为二进制文件 |

 对于目录：

| 权限名称 |               可执行操作 |
| :------- | -----------------------: |
| r        |       可以查看目录下列表 |
| w        | 可以创建和删除目录下文件 |
| x        |       可以使用cd进入目录 |

**需要注意的是超级用户可以无视普通用户的权限，即使文件目录权限是000，依旧可以访问。**
**在linux中的每个用户必须属于一个组，不能独立于组外。在linux中每个文件有所有者、所在组、其它组的概念。**

- **所有者**

  一般为文件的创建者，谁创建了该文件，就天然的成为该文件的所有者，用ls ‐ahl命令可以看到文件的所有者 也可以使用chown 用户名  文件名来修改文件的所有者 。

- **文件所在组**

  当某个用户创建了一个文件后，这个文件的所在组就是该用户所在的组 用ls ‐ahl命令可以看到文件的所有组 也可以使用chgrp  组名  文件名来修改文件所在的组。 

- **其它组**

  除开文件的所有者和所在组的用户外，系统的其它用户都是文件的其它组 

> 我们再来看看如何修改文件/目录的权限。

**修改文件/目录的权限的命令：`chmod`**

示例：修改/test下的aaa.txt的权限为属主有全部权限，属主所在的组有读写权限，
其他用户只有读的权限

**`chmod u=rwx,g=rw,o=r aaa.txt`**

**`chmod -R u=rwx,g=rwx,o=rwx ./log`** // 递归给log目录下的所有文件授权

![](../media/pictures/Linux.assets/164697447dc6ecac)

上述示例还可以使用数字表示：

chmod 764 aaa.txt

**补充一个比较常用的东西:**

假如我们装了一个zookeeper，我们每次开机到要求其自动启动该怎么办？

1. 新建一个脚本zookeeper
2. 为新建的脚本zookeeper添加可执行权限，命令是:`chmod +x zookeeper`
3. 把zookeeper这个脚本添加到开机启动项里面，命令是：` chkconfig --add  zookeeper`
4. 如果想看看是否添加成功，命令是：`chkconfig --list`

## Vim 编辑器

**Vi Vim 三种模式转换图** 

这个和上面的vim内容有点出入!以上面为主!

![1570193672730](../media/pictures/Linux.assets/1570193672730.png)

在任何状态下，按下Esc切换到命令模式，此模式下可以使用，指定插入位置，删除指定内容（dd），复制（yy），粘贴（pp），撤销（u）等命令。

在git的使用中!git push,有时候如果发生冲突,进入Vim中,需要退出来一般按:wq即可!



- Vim有三种模式：命令行模式，插入模式，底行模式
- 命令模式：使用vim命令打开一个文本文件，默认是命令模式。
- 底行模式：在命令模式下，按下：（冒号）切换到底行模式，在底行模式下，可以执行保存，退出等命令。
- 插入（编辑）模式：在命令模式下，按a或i或o（大小写都可以，但意义不同）可切换到插入模式，在此模式下，我们可以编辑文件内容。



**命令状态下：演示如下命令**：

- i在关标位置开始插入字符。 Insert
- I在光标所在行的最前面开始加字。
- a在光标位置后开始加字。
- A 在光标所在行的最后面开始加字。
- o在光标下加一空白行并开始加字。
- O 在光标上加一空白行并开始加字。
- Shift+h(H):光标移到屏幕的第一行
- Shift+l(L):光标移到屏幕的最后一行
- w:向后移动一个单词
- :number :指定到某一行
- b:向前移动一个单词
- dd：删除一行
- yy或Y :可以把一行文本拷贝到寄存器中
- Pp或p :粘贴一行

为了方便演示，在介绍一个命令wget -P 指定目录
资源地址，下载某资源到指定目录（就下载百度首页的html）



## 重定向

![1594436302957](../media/pictures/Linux.assets/1594436302957.png)

图片是鸟哥私房菜里面的图片，这个画的很好。

图片中，上面两个代表标准输入，标准输出。下面代表标准错误输出。

- **`标准输入（stdin）`**：代码0，使用 < 或者 <<
- **`标准输出（stdout）`**：代码1，使用 > 或者 >>
- **`标准错误输出（stderr）`**：代码2，使用2> 或者2>>



- **`>`**: 将某命令的标准输出重定向到另外的地方，通常是别的文件中。
  - ls -l \> a 将当前某目录下的文件或目录的详细信息，保存到a文件中
- **`>>`** : 和 \>不同的是，这种重定向表示，在目标原有的基础上，**追加新增的内容，而不是覆盖原有的内容**
- **`<<`** : 表示从键盘输入（标准输入），以\<\<后面的内容作为结束符  cat > d << ”oo“ 查找文件，表示由cat将输入的信息直接输出到d文件中，以oo结束（输入两个不代表追加，代表结束 ）
- **`<`** :将标准输入流即键盘输入，转化为\<之后的的数据源，比如文件 cat > file < ~/.bashrc , 这种就表示由文件中输入，而不是键盘输入。



小总结：

向右的有四种，一个箭头的不追加，两个的追加。

箭头向左的，有两种，两个的表示以一个字符结尾。一个一般直接表示输入。



## 常见的系统命令

```shell
date #查看系统时间
date -s "yyyy-MM-dd HH:mm:ss"

clear #清理屏幕
ctrl + l # 清屏 这个好用 
```



## 查看进程信息：

这个博客里面 有详细的查看进程 下面那个个不全 

```shell
#查看进程
ps -aux  #这个命令查出来的信息比较全面
ps -ef #查看所有进程 process status
ps -ef | grep xxx #查看所有满足筛选条件的进程
ps -aux | grep java #这个也可以查看满足条件的进程


#结束进程
Kill xxx：结束进程号为xxx的进程
Kill -9 xxx：强制结束进程号为xxx的进程
```

参考：https://blog.csdn.net/MaxineZhou/article/details/80468608?depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2&utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2





## 网络管理

```shell
ifconfig #查看网络设置
ifconfig 网卡名称 down  用网卡
ifconfig 网卡名称 up  用网卡

ping www.baidu.com #查看网络性

netstat -ano | grep 3306 #查看网络端口
sudo netstat -anp |grep 3306 #显示进程名称

```



## 用户管理

Linux系统是一个多用户多任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。

用户的账号一方面可以帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。

**Linux用户管理相关命令:**  （这些命令只有root可以操作）

- `useradd 选项 用户名`:添加用户账号
- `userdel 选项 用户名`:删除用户帐号
- `usermod 选项 用户名`:修改帐号
- `passwd 用户名`:更改或创建用户的密码
- `passwd -S 用户名` :显示用户账号密码信息
- `passwd -d 用户名`:  清除用户密码

useradd命令用于Linux中创建的新的系统用户。useradd可用来建立用户帐号。帐号建好之后，再用passwd设定帐号的密码．而可用userdel删除帐号。使用useradd指令所建立的帐号，实际上是保存在/etc/passwd文本文件中。

passwd命令用于设置用户的认证信息，包括用户密码、密码过期时间等。系统管理者则能用它管理系统用户的密码。只有管理者可以指定用户名称，一般用户只能变更自己的密码。



注意：

su 用户名 sudo 后面的这条命令 用管理员权限去执行

注意：安装linux 的时候root用户默认没有设置密码，此时直接su
切换到root用户会失败，应该先给root账号设置密码：如下

![](../media/pictures/Linux.assets/d5176c510de0016c33e9762c7be94524.png)



## Linux系统用户组的管理

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux 系统对用户组的规定有所不同，如Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。

用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对/etc/group文件的更新。

**Linux系统用户组的管理相关命令:**

- `groupadd 选项 用户组` :增加一个新的用户组
- `groupdel 用户组`:要删除一个已有的用户组
- `groupmod 选项 用户组` : 修改用户组的属性



# Linux Install Software

自从学了Docker，就用Docker装啦，装啥都很快。

## Jdk

- 首先，测试本地是否已经安装了jdk，利用java或javac命令来确认。
- 未发现本机安装有jdk，此时，从oracle官网下载linux版本的jdk

![](../media/pictures/Linux.assets/4522529703b64b566bc4622daa958003.png)

- 利用winscp工具，将下载好的jdk上传到家目录下

![](../media/pictures/Linux.assets/a4be8cf7c868cde0eea597bd906dcf21.png)

- 将jdk所在的tar文件解压到 \~/java目录中

![](../media/pictures/Linux.assets/96c9107964eb3d206e15c9a2f83bdf91.png)

![](../media/pictures/Linux.assets/32e2307c2a9c597820c0d1f51079293e.png)

- 将java目录移动到/usr/local/ 目录下

![](../media/pictures/Linux.assets/7545ae6ba67bafec44dbe02b3e652c98.png)

- 在/etc/profile 中配置环境变量

![](../media/pictures/Linux.assets/4572a56df334d023071219aa8752372b.png)



**进去以后 首先需要按i 转换成插入模式**

然后才可以编辑配置文件、

![](../media/pictures/Linux.assets/4bdbefb184fc64899c1a3312e624a7cf.png)

**编辑完：wq**



- 使配置文件立即生效，并测试配置的环境变量

![](../media/pictures/Linux.assets/9b176c581d5d7eb3465ef152e3c8905b.png)

![](../media/pictures/Linux.assets/37f991cf3f3de4eb28f0a0eee08b39f4.png)

如果不小心把冒号写成了分号

![](../media/pictures/Linux.assets/2cbb1f0e0d5bc443308a5868488f069e.png)

如果你需要在linux下配置IDEA 或者linux下编译程序

- 修改系统默认的javc命令配置（可选）

![](../media/pictures/Linux.assets/502a13e396a7becaa1f78fc4591a497c.png)

- 修改系统默认的java命令配置（可选）

![](../media/pictures/Linux.assets/30ab208429ef53e4b13bb30b11aa8b37.png)

## Tomcat的安装

- 下载tomcat 8.x的linux版本的包
- 通过winscp把tomcat所在的tar文件，传到建目录下的tomcat文件夹中

![](../media/pictures/Linux.assets/6ca1520a93db261c8355dde7e2178297.png)

- 解压并抽取该包

![](../media/pictures/Linux.assets/a894f6db1e85434fadf4a475ef3eb995.png)

![](../media/pictures/Linux.assets/515483147eaeb36cc901d31e5d3804c1.png)

- 将tomcat文件夹移动到/usr/local/目录下
- 启动tomcat，和windows中一样，主要是使用tomcat的bin目录中的startup工具

![](../media/pictures/Linux.assets/08489561319594e263e446cb2c7c2718.png)

![](../media/pictures/Linux.assets/b5ea2d97dad01eaca4f1c455b1e512df.png)

![](../media/pictures/Linux.assets/64fedefd9fefea331785802b69ad6ccb.png)

执行shell脚本

./startup.sh

- 测试tomcat服务器，在windows上连接成功

![](../media/pictures/Linux.assets/f09b7b82df6af8c767f1e6faee5ebf3d.png)

- 关闭tomcat

![](../media/pictures/Linux.assets/533821fa189a882edf949d4201a4c883.png)

./shutdown.sh

sh shutdown.sh

## Mysql的安装

- 首先检查是否本地有安装mysql

![](../media/pictures/Linux.assets/21eb6363f73385c3d3dc2acf74d2a183.png)

- 本地没有安装mysql，使用apt工具来安装mysql

![](../media/pictures/Linux.assets/29d470f2b21b955677a5e640763d1afb.png)

回去服务器获取安装程序，并开始安装。

过一会儿，弹出如下界面：

设置mysql的密码 :123456

![](../media/pictures/Linux.assets/9e05fab28b3e4f99754810ce2143f25a.png)

![](../media/pictures/Linux.assets/073032b5fb023defc34aaa681d69079e.png)

- 启动mysql测试是否安装成功

![](../media/pictures/Linux.assets/fa1f04fc2b5cfe0483593e02ba8b0835.png)

> 一般情况下数据库服务器是一台单独的服务，所以需要设置下远程连接。

### 配置远程访问(可选)

- 紧接着，设置在远程访问linux的mysql，这个设置分为2个部分，

> 第1部分是要修改mysql的配置文件，使得除本机之外的ip可以访问到数据库；

> 第2个部分是要在mysql中修改，给予root用户从别的主机上访问数据库的权限。

![](../media/pictures/Linux.assets/7d932890649e5d58094e220c6fe355c4.png)

此处，将bind-address修改为0.0.0.0，原本是127.0.0.1即本机

![](../media/pictures/Linux.assets/e9fbba5e22dd8245d5e1c453a677c8bb.png)

重启mysql服务，使配置生效

![](../media/pictures/Linux.assets/e57ee50361a34b51ee72b02c3937a562.png)

进入mysql，给远程连接授予权限

修改为自己的用户密码 (这里密码1234必须改成自己的密码！)



**2020/1/19 实际测试，如果没有下面这一句 用navicat 连接不上**  

进 mysql里面 

```java
mysql -uroot -p123456

```

```
mysql> grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option ;

```

弄完以后 要**重新启动一下mysql**

```
sudo /etc/init.d/mysql restart

```



![](../media/pictures/Linux.assets/53f42b960e322ad4832fb4fe2683ae5b.png)

查询设置的结果：

![](../media/pictures/Linux.assets/5a551616a89f4093cf84bffdf12c35bd.png)

使配置文件，立即生效

![](../media/pictures/Linux.assets/7efd169d5946cee34537addef5568121.png)

在windows上用yog客户端连接，linux上的mysql服务器

![](../media/pictures/Linux.assets/826d7b8927eefc436fdbe7e50e9c899c.png)

如下配置：mysql是否为开机启动

- 查看mysql是否为开机启动，为此，简单起见，我们使用一t个服务管理程序sysv--rc-conf

![](../media/pictures/Linux.assets/da814fbba4755caa0ccb72a858f2cb92.png)

- 启动该工具，查看mysql的运行状态，
- 可以通过查看3306端口号
- 或者查看mysql进程有没有启动
- 可以看到多用户状态下（运行级别2-5），mysql已经开启开机启动

![](../media/pictures/Linux.assets/53369736af1c34bfc759d78e6e8e4e96.png)

[Linux](http://lib.csdn.net/base/linux) 系统任何时候都运行在一个指定的运行级上，不同的运行级的程序和服务都不同，所要完成的工作和要达到的目的都不同，系统可以在这些运行级之间进行切换，以完成不同工作。

![](../media/pictures/Linux.assets/6e1084cf423f1a5fb3b1359eb1444433.png)

来看一下，我们当前的运行级别

![](../media/pictures/Linux.assets/ba2236d92a66c20a081ba18ce9123eaf.png)



## redis

### 一、在阿里云服务器上安装redis:

　　1.下载　　wget http://download.redis.io/releases/redis-4.0.9.tar.gz

　　2.解压　　tar xzf redis-4.0.9.tar.gz

　　3.跳转目录　　cd redis-4.0.10

　　4.安装　　make

　　5.启动服务端：src/redis-server

　　6.启动客户端：src/redis-cli

### 二、在阿里云服务器上添加安全规则:

　　1.实例---更多---网络安全组---安全组配置

![img](../media/pictures/Linux.assets/1271078-20191209204758525-1476685704-1584272664981.png)

　　2.配置安全规则

　　　　　　　　　　![img](../media/pictures/Linux.assets/1271078-20191209204814612-761830068-1584272664989.png)

### 三、配置redis.conf

　　1.进入配置文件  vim redis.conf

　　2.注释掉绑定ip bind 127.0.0.1   #不注释的话就是默认只允许本地访问

　　3.将保护模式改成no  daemonize yes   设置为no

 

### 四、给redis设置密码，命令如下：

　　1.127.0.0.1:6379> config get requirepass

​        　　1) "requirepass"

​        　　2) ""

 

　　2.为以上显示说明没有密码，那么现在来设置密码：

​     　　127.0.0.1:6379> config set requirepass dyydyy //密码是dyydyy

​      　　OK

​     　　127.0.0.1:6379> 

 

　　3.再次查看当前redis就提示需要密码：

​       　　127.0.0.1:6379> config get requirepass

​       　　(error) NOAUTH Authentication required.

​       　　127.0.0.1:6379>

​       　　*注意：阿里云上部署的redis需要设置密码，这样本地redis的客户端Redis Desktop Manager才可以连上，添加的时候要填写密码。

　　4.使用密码连接，跳转至src下   cd src，执行命令：./redis-cli -h 127.0.0.1 -p 6379 -a 密码

 

### 五、本地redis的客户端Redis Desktop Manager测试连接，添加的时候要填写密码

　　　　　　　　　　　　　　　　　　![img](../media/pictures/Linux.assets/1271078-20191209210052183-1059684253-1584272665038.png)



## Nginx

首先需要,弄两个以上的tomcat ,使用cp -r apache-tomcat-8.5.16 tomcat2 ,如果需要复制文件夹,中间必须加-r,否则不能复制!

![1570711044867](../media/pictures/Linux.assets/1570711044867.png)



### 开启两个tomcat:

需要修改几个地方:1.首先需要修改端口为8090

![1570713359592](../media/pictures/Linux.assets/1570713359592.png)

2.然后需要修改server port

![1570713450288](../media/pictures/Linux.assets/1570713450288.png)

这两个地方需要修改,然后就可以通过浏览器访问啦!



配置Nginx 首先需要配置这个地方:

![1570709611127](../media/pictures/Linux.assets/1570709611127.png)

打开配置两个地方:首先打开,配置这个,这里upstream后面名字是随便起得!这里起域名翻转是为了不重复

​                                                  !![1570709669226](../media/pictures/Linux.assets/1570709669226.png)

还需要在location里面加这一句话:意思是进行转发,代理

![1570709790077](../media/pictures/Linux.assets/1570709790077.png)

然后将nginx下面的nginx.conf下面修改成两个tomcat,

然后输入命令重新加载nginx, 

![1570713905845](../media/pictures/Linux.assets/1570713905845.png)

加了这句,在使用的时候,可以抓包,不然不能抓包!

这两句话,一句表示增加响应头,一句表示增加相应状态!

![1570714756142](../media/pictures/Linux.assets/1570714756142.png)

加了这两句话然后执行 ./nginx -s reload, 就可以重新加载啦!

报文里面加了相应头!和状态码!

![1570715115095](../media/pictures/Linux.assets/1570715115095.png)



用vim时候,如果某一步操作错误,强制退出**:q!**

这样的话,不会修改原来文件的东西!不会保存!

再次进入重新编辑即可!



## Ubuntu搭建Zookeeper服务



### 1、下载安装包

官方下载地址http://apache.fayea.com/zookeeper/

### 2、安装

安装前确保系统已安装过JDK，[JDK安装过程可参照](https://www.cnblogs.com/kingsonfu/p/9801556.html)

2.1 解压下载好的tar.gz安装包到某个目录下，可使用命令：

```shell
tar -zxvf zookeeper-3.5.4-beta.tar.gz

```

2.2 进入解压目录的conf目录，复制配置文件zoo_sample.cfg并命名为zoo.cfg，相关命令为：

```shell
cp zoo_sample.cfg zoo.cfg

```

2.3 编辑zoo.cfg文件

```shell
vi zoo.cfg

```

主要修改如下：

```shell
# 增加dataDir和dataLogDir目录，目录自己创建并指定，用作数据存储目录和日志文件目录
dataDir=/home/local/zk/data
dataLogDir=/home/local/zk/logs
# 指定server地址，server.id=hostname:port:port。第一个端口用于集合体中的 follower 以侦听 leader；第二个端口用于 Leader 选举。第一个hostname即为本服务器地址
server.1=192.168.242.131:2888:3888

```

2.4 修改好zoo.cfg配置之后，在创建好的data目录中添加myid文件，里面的内容设置为zoo.cfg中配置的server.1中的数字，即1，有多台可以进行类似配置。

2.5 配置系统环境变量

```shell
vi /etc/profile

```

添加

```shell
export ZOOKEEPER_HOME=/home/kinson/zk 
PATH=$ZOOKEEPER_HOME/bin:$PATH

```

使添加的配置其生效

```shell
source /etc/profile

```

2.6 服务启动及客户端相连，最好是在root用户下启动

```shell
zkServer.sh start

```

启动完之后可以查看启动状态

```shell
zkServer.sh status

```

客户端连接

```shell
zkCli.sh -server localhost:2181

```

连接成功如下图：

![img](../media/pictures/Linux.assets/761230-20190331142727565-746364350.png)

之后就可以使用一些基础命令，比如 ls，create，delete，get 来测试了。

### 3、ZK常用命令

3.1 ZK服务命令

```shell
# 启动ZK服务       
zkServer.sh start
# 查看ZK服务状态 
zkServer.sh status
# 停止ZK服务       
zkServer.sh stop
# 重启ZK服务       
zkServer.sh restart

```

3.2 ZK客户端命令

```shell
# 显示根目录下、文件： 
ls /  #使用ls命令来查看当前ZooKeeper中所包含的内容
# 显示根目录下、文件： 
ls2 /  #查看当前节点数据并能看到更新次数等数据
# 创建文件，并设置初始内容：
create /zk "kinson"  #创建一个新的znode节点"zk"以及与它关联的字符串
# 获取文件内容： 
get /zk  # 确认 znode 是否包含我们所创建的字符串
# 修改文件内容： 
set /zk "king"  #对zk所关联的字符串进行设置
# 删除文件 
delete /zk  #将znode节点zk删除
# 退出客户端： 
quit
# 帮助命令： 
help

```



参考：https://www.cnblogs.com/kingsonfu/p/10631332.html

https://blog.csdn.net/weixin_40570311/article/details/98641035

## Ubuntu安装Docker

### Ubuntu 14.04 16.04 (使用apt-get进行安装)

```shell
# step 1: 安装必要的一些系统工具
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
# step 2: 安装GPG证书
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# Step 3: 写入软件源信息
sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# Step 4: 更新并安装 Docker-CE
sudo apt-get -y update
sudo apt-get -y install docker-ce

注意：其他注意事项在下面的注释中
# 安装指定版本的Docker-CE:
# Step 1: 查找Docker-CE的版本:
# apt-cache madison docker-ce
#   docker-ce | 17.03.1~ce-0~ubuntu-xenial | http://mirrors.aliyun.com/docker-ce/linux/ubuntu xenial/stable amd64 Packages
#   docker-ce | 17.03.0~ce-0~ubuntu-xenial | http://mirrors.aliyun.com/docker-ce/linux/ubuntu xenial/stable amd64 Packages
# Step 2: 安装指定版本的Docker-CE: (VERSION 例如上面的 17.03.1~ce-0~ubuntu-xenial)
# sudo apt-get -y install docker-ce=[VERSION]

# 通过经典网络、VPC网络内网安装时，用以下命令替换Step 2、Step 3中的命令
# 经典网络：
# curl -fsSL http://mirrors.aliyuncs.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyuncs.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# VPC网络：
# curl -fsSL http://mirrors.cloud.aliyuncs.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# sudo add-apt-repository "deb [arch=amd64] http://mirrors.cloud.aliyuncs.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"

```



### CentOS 7 (使用yum进行安装)

```shell
# step 1: 安装必要的一些系统工具
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
# Step 2: 添加软件源信息
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# Step 3: 更新并安装 Docker-CE
sudo yum makecache fast
sudo yum -y install docker-ce
# Step 4: 开启Docker服务
sudo service docker start

注意：其他注意事项在下面的注释中
# 官方软件源默认启用了最新的软件，您可以通过编辑软件源的方式获取各个版本的软件包。例如官方并没有将测试版本的软件源置为可用，你可以通过以下方式开启。同理可以开启各种测试版本等。
# vim /etc/yum.repos.d/docker-ce.repo
#   将 [docker-ce-test] 下方的 enabled=0 修改为 enabled=1
#
# 安装指定版本的Docker-CE:
# Step 1: 查找Docker-CE的版本:
# yum list docker-ce.x86_64 --showduplicates | sort -r
#   Loading mirror speeds from cached hostfile
#   Loaded plugins: branch, fastestmirror, langpacks
#   docker-ce.x86_64            17.03.1.ce-1.el7.centos            docker-ce-stable
#   docker-ce.x86_64            17.03.1.ce-1.el7.centos            @docker-ce-stable
#   docker-ce.x86_64            17.03.0.ce-1.el7.centos            docker-ce-stable
#   Available Packages
# Step2 : 安装指定版本的Docker-CE: (VERSION 例如上面的 17.03.0.ce.1-1.el7.centos)
# sudo yum -y install docker-ce-[VERSION]
# 注意：在某些版本之后，docker-ce安装出现了其他依赖包，如果安装失败的话请关注错误信息。例如 docker-ce 17.03 之后，需要先安装 docker-ce-selinux。
# yum list docker-ce-selinux- --showduplicates | sort -r
# sudo yum -y install docker-ce-selinux-[VERSION]

# 通过经典网络、VPC网络内网安装时，用以下命令替换Step 2中的命令
# 经典网络：
# sudo yum-config-manager --add-repo http://mirrors.aliyuncs.com/docker-ce/linux/centos/docker-ce.repo
# VPC网络：
# sudo yum-config-manager --add-repo http://mirrors.could.aliyuncs.com/docker-ce/linux/centos/docker-ce.repo

```



### 安装校验

```shell
root@iZbp12adskpuoxodbkqzjfZ:$ docker version
Client:
 Version:      17.03.0-ce
 API version:  1.26
 Go version:   go1.7.5
 Git commit:   3a232c8
 Built:        Tue Feb 28 07:52:04 2017
 OS/Arch:      linux/amd64

Server:
 Version:      17.03.0-ce
 API version:  1.26 (minimum version 1.12)
 Go version:   go1.7.5
 Git commit:   3a232c8
 Built:        Tue Feb 28 07:52:04 2017
 OS/Arch:      linux/amd64
 Experimental: false

```

启动docker服务：

```
# service docker start

```



### 配置阿里云镜像

需要登录阿里云https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors 开发者镜像

然后选择镜像加速器

![1591176559020](../media/pictures/Linux.assets/1591176559020.png)

然后按照下面的进行操作。



检查加速镜像是否生效： （这个命令在Ubuntu上面看不出来是否用的阿里云镜像），用下面的命令

```
ps -ef|grep docker

```

CentOS测试出来是这个样子的 可以看到阿里云镜像

![1591177347632](../media/pictures/Linux.assets/1591177347632.png)

但是乌班图测试出来是这个2样子的，看不出来是否用的阿里云镜像

![1591177398374](../media/pictures/Linux.assets/1591177398374.png)



自己测试发现上面这个看不出来，用下面这个命令

```
docker info 使用这个可以看得出来，仓库配置的是阿里云的加速仓库。

```

![1591177166624](../media/pictures/Linux.assets/1591177166624.png)



### 参考资料

其他关于旧版本Docker卸载以及测试开发版本Docker安装的帮助，可以参考官方文档的说明进行安装

- [CentOS帮助链接](https://yq.aliyun.com/go/articleRenderRedirect?url=https%3A%2F%2Fdocs.docker.com%2Fengine%2Finstallation%2Flinux%2Fdocker-ce%2Fcentos%2F)
- [Ubuntu帮助链接](https://yq.aliyun.com/go/articleRenderRedirect?url=https%3A%2F%2Fdocs.docker.com%2Fengine%2Finstallation%2Flinux%2Fdocker-ce%2Fubuntu%2F)
- [Debian帮助链接](https://yq.aliyun.com/go/articleRenderRedirect?url=https%3A%2F%2Fdocs.docker.com%2Fengine%2Finstallation%2Flinux%2Fdocker-ce%2Fdebian%2F)
- [Fedora帮助链接](https://yq.aliyun.com/go/articleRenderRedirect?url=https%3A%2F%2Fdocs.docker.com%2Fengine%2Finstallation%2Flinux%2Fdocker-ce%2Ffedora%2F)

### 源站使用问题

云栖社区文章下的评论不会实时通知，所以更新文章的时候才发现有用户在使用中遇到了各种各样的问题。
目前源站每日凌晨更新，如果有源站使用问题例如文件损坏、文件不存在、版本滞后超过两天等问题，请发送邮件至 hyzhou.zhy@alibaba-inc.com，邮件标题包含“Docker CE 镜像源站”。附上安装机器的网络环境，执行命令以及错误提示信息。或者直接扫码联系钉钉账户最佳。



参考：

https://blog.csdn.net/xie1xiao1jun/article/details/79413436

https://yq.aliyun.com/articles/110806



### 运行HelloWorld 

```
docker run hello-workd

```

![1591178116508](../media/pictures/Linux.assets/1591178116508.png)





## 集群的session共享

### Session共享问题

使用了Nginx和集群，对客户端的请求做了负载均衡，从系统的吞吐量的角度来看，这无疑是很好的，但是，随之而来的一个问题，就是session共享的问题：

![](../media/pictures/Linux.assets/112e3b6ba93accf2df7873d1f2b7731a.png)

如图，在浏览器的一次会话中，两次访问Nginx代理的集群，Nginx分别把这两次请求，分配给了不同的服务器来处理，于是出现了这样一个问题：

- 首先，session只产生和存在于单个服务器中。
- 明明是逻辑上的一次会话，因为实际访问了两台不同的服务器，所以两台服务器会分别为针对它们各自的请求而新建会话（假设两台服务器都是被该浏览器第一次访问）。
- 于是，一次会话的信息，实际上被两个服务器中的两个session所存储，每个session实际只存储，这次会话的部分信息。
- 这种情况下，我们通过nginx访问同一个页面多次，可能会访问不同服务器上的同一个页面，session不同步的问题会导致用户必须在同一个页面登录两次。

## Session共享问题的解决

### Session sticky

这种解决方案的思路，比较简单，就是用一个hash算法，将对某ip的访问映射到一台确定的服务器上，这样针对某ip的访问就固定到一台确定的服务器，不同的ip访问不同的服务器。

同时，这种解决方案也有一定的局限性：

- 一旦tomcat所在的某台服务器重新启动，那么与这台服务器相关的会话信息就会丢失，如果用户此时再次访问相同网页，需要重新登录。高可用不满足。
- 代理服务器需要计算，保存，维护ip和相应服务器之间的映射关系，内存消耗大。

### Session Replication 高可用

这种解决方案的思路是，每个服务器上，都有集群中其他服务器中session数据的副本，同时增加服务器之间的数据同步功能，通过服务器之间的同步保证session数据在各个服务器之间的一致性。

这种解决方案，不再像session
sticky中那样要求Nginx服务器做一些处理，但是这种方式的局限性也很大：

- 一旦session数据发生变化，所有的服务器都需要同步变化的session数据，而这种同步会消耗带宽。
- 同时，由于每台服务器都存储了其他所有服务器上的session副本，
  冗余数据也占用了服务器的存储空间

<https://www.2cto.com/net/201701/584323.html>

两个关键配置：

两个Tomcat的server.xml

![](../media/pictures/Linux.assets/75e1305b18303dd71c3967a8f6312874.png)

两个应用的web.xml

![](../media/pictures/Linux.assets/67cfb9d6884ffb9b460b08b568c291bd.png)

访问的url

<http://192.168.5.75/Session2/test>

### Session数据集中控制

这种解决方案的思路是，将所有服务器上的session数据集中存储和管理，这样一来，所有的服务器的session在集群中只需要有一份。

这种解决方案，由于session并不存储在本地，对session的访问需要通过网络，这样可能就会产生访问的延时，以及不稳定性，不过我们通信基本都是发生在内网，问题不大，如果集中存储Session的机器或者集群有问题，就会影响我们的应用。

Redis 内存数据库 Nosql

### Cookie based

这种解决方案的思路是，将session数据保存到cookie中，当浏览器访问服务器的时候，服务器可以从cookie中再生成相应的session信息。

这种方式，也有其局限性：

- Cookie长度的限制：我们都知道Cookie是有长度限制的，而这回限制Session数据的长度。
- 安全性。Session数据本来都是服务端数据，而这个方案是让这些服务端数据写到了到了外部网络以及客户端，因此存在安全性上的问题，我们可以对写入Cookie的Session数据做加密，不过对于数据安全来说，物理上不能接触才是安全的。
- 带宽消耗：这里指的不是内部Web服务器之间的带宽消耗，而是我们数据中心的整体外部带宽的消耗



# Ailiyun Linux

## 3.商城项目springboot项目jar包放到了home/jar下面



## 4、springboot打成的jar如何在Linux上持久运行

首先呢？你本地要有一个springboot的项目，如果没有可以参考我的这篇博客写一个,[springboot入门程序](https://www.cnblogs.com/youcong/p/8098861.html)

然后呢？你要有一个虚拟机搭建一个Linux服务器或者是远程服务器(阿里云或者腾讯云、百度云、美团云等)。

再然后，你还要有一个winscp，winscp官网地址为:https://winscp.net/eng/docs/lang:chs(你可以去官网下载)

最后将springboot打包(确保本地运行没有问题)，利用winscp上传到Linux上。

通过该命令运行jar包:

```html
nohup java -jar blog.jar > system.log 2>&1 &

```

下面我们对这条命令进行分析

nohub一般形式为如下:

nohub command &

但是当你退出账户时，仍然会停止对应的进程。

所以这就需要你在后面添加 2>&1 &(相当于正常退出，仍保持命令在后台运行)

上面这个command正好对上java -jar blog.jar > system.log

“>” 输出重定向，通常用于输出日志

使用命令：ps -a可以查看Java程序运行的进程号，用于停止程序，不过当程序有好几个的时候，用命令：ps -ef|grep java这个命令会将搜索Java相关的所以进程号，根据jar包名称找到需要停止的进程号，使用命令：kill -9 11759杀死进程，11759是进程号。（PS：杀死进程时一定要注意不要看错了进程号，以免杀错！！）



## 5.每一次部署项目  记得要去阿里云打开这个项目对应的端口 

**切记**

## 6.Vue项目打包成移动端APP

https://blog.csdn.net/Li_dengke/article/details/101385345

## 7.修改阿里云服务器名

- 查看当前主机名：**hostname**

[![查看主机名](../media/pictures/Linux.assets/16853007-f7e6264b63fcd4ee.png)](https://upload-images.jianshu.io/upload_images/16853007-f7e6264b63fcd4ee.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

- 修改主机名：**hostnamectl set-hostname 修改后的主机名**

[![修改主机名](../media/pictures/Linux.assets/16853007-49be845eef42f030.png)](https://upload-images.jianshu.io/upload_images/16853007-49be845eef42f030.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

修改后，再次输入 **hostname** 可发现主机名已经被修改了，但当前会话界面的还是原来的名称，这里我们只需要重新建立会话连接，或者直接重启服务器就行了

- 重启服务器

[![修改成功](../media/pictures/Linux.assets/16853007-c6396079fc7b69aa.png)](https://upload-images.jianshu.io/upload_images/16853007-c6396079fc7b69aa.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

OK，到这里已成功完成了主机名的修改，大功告成！



## 8.查看阿里云服务器cpu 内存使用

**查看CPU使用**

```shell
top

```

![1585882274571](../media/pictures/Linux.assets/1585882274571.png)

**查看内存**

```shell
free -m

```

![1585882387300](../media/pictures/Linux.assets/1585882387300.png)





阿里云买新域名，记得要实名注册和解析

阿里云OSS，记得要设置 Access key ，简历bucket

同时可以用软件OSSBrowser管理图片

![1591783245122](../media/pictures/Linux.assets/1591783245122.png)

这是参考说明文档。里面很详细。



## 9 CDN 

### 不知道这是不是阿里云服务器里面的知识，先放在这里

开通**CDN**,加载速度会很快!会将资源放置在离你最近的节点上面!



# VMware

## CnetOS 7 

安装虚拟机15，系统之家下载系统，安装CentOs7。

看CodeSheep，结合https://blog.csdn.net/babyxue/article/details/80970526



### 搞好以后，网络需要选桥接

```
su root  //root

dhclient  //用这个讲虚拟机的地址固定下来  以后使用方便

ifconfig //这时候就有IP地址啦
```

![1590472209216](../media/pictures/Linux.assets/1590472209216.png)



接下来的操作是让虚拟机的IP固定下来，不要变化。方便后面使用，所以要在网卡里面写死。

修改网卡:

```
vim /etc/sysconfig/network-scripts/ifcfg-ens33 
```

如果不知道是那个文件夹下 可以快速两下tab 文件提示 ：

![1590473033816](../media/pictures/Linux.assets/1590473033816.png)



![1590472915527](../media/pictures/Linux.assets/1590472915527.png)



上面设置的信息依次是 IP地址，子网掩码，网关，DNS服务解析

设置好了 ，重启网络

```
systemctl restart network.service
```



### centos7 关闭防火墙

```shell
sudo systemctl stop firewalld 临时关闭

sudo systemctl disable firewalld ，然后reboot 永久关闭

sudo systemctl status  firewalld 查看防火墙状态。
```



## Ubuntu

### 桌面版

#### 修改屏幕显示比例:

虚拟机上装ubuntu,修改屏幕显示比例 ,中间的x是字母x!



![1570591412484](../media/pictures/Linux.assets/1570591412484.png)





# 面试题

### 1.Linux下如何启动springboot的包？

```html
nohup java -jar blog.jar > system.log 2>&1 &

```

下面我们对这条命令进行分析

nohub一般形式为如下:

nohub command &

但是当你退出账户时，仍然会停止对应的进程。

所以这就需要你在后面添加 2>&1 &(相当于正常退出，仍保持命令在后台运行)

上面这个command正好对上java -jar blog.jar > system.log

“>” 输出重定向，通常用于输出日志



### 2.linux命令（怎么查看linux中当前各个进程占用的系统资源）

```shell
ps -aux

```



### 3.说几个常用的linux命令 ,五个以上，用途

1.目录切换

```java
cd 文件夹 //进入某一个文件夹
cd .. //返回上一级目录

```

2.目录操作 

```shell
mkdir //增加目录
ll/ls //查看目录下文件
rmdir //删除文件

```

3.文件操作

```shell
1. touch 文件名称   //文件的创建（增）
2. cat/more/less/tail 文件名称  //文件的查看（查）

```

4.压缩和解压

（1）压缩

Linux中的打包文件一般是以.tar结尾的，压缩的命令一般是以.gz结尾的。

而一般情况下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。
命令：**`tar -zcvf 打包压缩后的文件名 要打包压缩的文件`**
其中：

  z：调用gzip压缩命令进行压缩

  c：打包文件

  v：显示运行过程

  f：指定文件名

比如：假如test目录下有三个文件分别是：aaa.txt bbb.txt ccc.txt，如果我们要打包test目录并指定压缩后的压缩包名称为test.tar.gz可以使用命令：**`tar -zcvf test.tar.gz aaa.txt bbb.txt ccc.txt`或：`tar -zcvf test.tar.gz       /test/`**

（2）解压

命令：tar [-xvf] 压缩文件

其中：x：代表解压

示例：

1 将/test下的test.tar.gz解压到当前目录下可以使用命令：**`tar -xvf test.tar.gz`**

2 将/test下的test.tar.gz解压到根目录/usr下:**`tar -xvf test.tar.gz -C /usr`**（- C代表指定解压的位置）

5.网络管理

```shell
ifconfig 查看ip地址
ping 地址 查看连接情况

```



### 4.linux命令查看服务器性能

**（1）查看CPU使用**

```shell
top

```

![1585882274571](../media/pictures/Linux.assets/1585882274571-1588243560477.png)

**（2）查看内存**

```shell
free -m

```

![1585882387300](../media/pictures/Linux.assets/1585882387300-1588243560479.png)



参考：https://blog.csdn.net/guoxiaojie_415/article/details/80526667?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-4&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-4 （写的算好的一篇  有参考其他）

https://netflixtechblog.com/linux-performance-analysis-in-60-000-milliseconds-accc10403c55 （国外的一个，需要梯子）

**（3）uptime 查看负载**

![1588237066015](../media/pictures/Linux.assets/1588237066015.png)

几个负载分别是1min，5min，15min的平均负载



### 5.Linux改变文件所属组的命令，生成文件的命令

https://www.cnblogs.com/klb561/p/9170616.html

[root@localhost ~]# chgrp group1 install.log

\#修改install.log文件的所属组为group1



[root@localhost user]# touch test

\#由root用户新建文件test



### 6.熟悉Linux什么指令？ 说一下如何把文件中的abc替换为def；说一下如何找出某文件夹下所有包含“abc”的文件？

参考：https://blog.csdn.net/Olivia_Vang/article/details/104091358?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1



### 7.Linux系统是32位还是64位查询命令

![1588240540192](../media/pictures/Linux.assets/1588240540192.png)

参考：https://www.cnblogs.com/nucdy/p/5658488.html 

### 8.Linux 方面，查日志：cat 命令，如果根据日期查怎么查，日志文件很大，快速定位错误日志(只给一个模糊时间)，我又说了 grep 和 管道符，面试官说这不是最好的。

下面这个是查询错误：

```shell
cat -n system.log | grep "error" //grep是搜索的意思  -n的意思是显示行号（大日志显示行号 很有必要）

```

![1588242904651](../media/pictures/Linux.assets/1588242904651.png)

查出来是这样的。

参考：https://www.cnblogs.com/woshixiangshang/p/11585306.html   （博客园上面的，写的还行）



**其实还有好多种查日志的方法：** （也很重要）

上面的cat命令显示全部，不太好，

还有more和less操作，都表示一页一页翻页，但是less操作起来好一点。

less空格和Pgdown向下翻页，pageup向上翻页