# Linux
## Linux 命令
- 查看系统语言： echo $LANG
- 查看系统安装的语言包： locale
- 查看系统时间和时区：date 或 date -R
- 安装中文语言包: yum groupinstall chinese-support
- 临时更换语言: LANG="en_US.UTF-8"   中文为（"zh_CN.UTF-8"）
- 修改系统默认的语言: vi /etc/sysconfig/i18n
- 在启动java程序时加参数-Duser.timezone=GMT+8
- 查看防火墙状态：firewall-cmd --state
- 开放80端口：firewall-cmd --zone=public --add-port=80/tcp --permanent
    - --zone #作用域
    - --add-port=80/tcp  #添加端口，格式为：端口/通讯协议
    - --permanent   #永久生效，没有此参数重启后失效
- 更新防火墙规则：firewall-cmd --reload
- 关闭防火墙： 
    - service firewalld stop
    - systemctl stop firewalld.service
- 禁止防火墙开机启动：systemctl disable firewalld.service
- 查看PID：
    - ps -ef | grep java
    - -v:表示忽略grep本身: ps -ef | grep java | grep -v grep
    - grep进程的条目显示处理命令优先于正则表达式: ps -ef | grep [j]ava
- 查看端口号：netstat -apn | grep PID
- awk把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理
- 查看nginx路径: ps aux | grep nginx
- 查看nginx配置文件路径: /usr/sbin/nginx -t

### which(命令)
- 查找命令路径 `which git`
- 查找命令对应的真实路径(可能是软连接) `ls -al /usr/bin/git`

### whereis(文件或命令)
- 查找文件或者命令的所在目录 `whereis mysql`

### find(文件或文件夹)
- 查找根目录查找包含“java”字符文件或文件夹 
`find / -name java`
- 查找在当前目录下，深度为一，以.jpg结尾文件，并将其转化
`find . -maxdepth 1 -name *.jpg -print -exec convert ` 
- 查找以 '.rpm' 结尾的文件并定义其权限
`find / -name *.rpm -exec chmod 755 '{}' \`
- 查找以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备
`find / -xdev -name \*.rpm`
- 查找系统中所有使用了SUID控制的文件
`ind / -perm -u+s`
- 查找属于用户 'user1' 的文件和目录
`find / -user user1` 
- 查找并复制所有以 '.txt' 结尾的文件到另一个目录
`find /home/user1 -name '*.txt' | xargs cp -av --target-directory=/home/backup/ --parents`  
- 查找在过去100天内未被使用过的执行文件
`find /usr/bin -type f -atime +100`
- 搜索在10天内被创建或者修改过的文件
`find /usr/bin -type f -mtime -10`
- 查找所有以 '.log' 结尾的文件并做成一个bzip包
`find /var/log -name '*.log' | tar cv --files-from=- | bzip2 > log.tar.bz2`

### yum(软件包)
- 查找软件包
`yum list docker`
- 查找已安装的软件包
`yum list installed`
- 所有已安裝的软件包信息
`yum info installed`

### rpm(软件包)
- 查找软件包
`rpm -q python`
- 查询某个包所有的安装文件
`rpm -ql python`
- 查找已安装的软件包
`rpm -qa`
- 查找软件包，根据命令
`rpm -qf java`
- 删除某个包
`rpm -e python`

### free
- 查看内存使用情况
  `free`
- 查看内存使用情况，M为单位
  `free -h`

### top

- 查看资源管理器

  `top`

- 查看指定用户的资源管理器

  `top -u root`

## Linux 文件
### Linux根目录”/“下各个系统文件夹的含义和用途

- /boot 该目录默认下存放的是Linux的启动文件和内核。
- /initrd 它的英文含义是boot loader initialized RAM disk,就是由boot loader初始化的内存盘。在linux内核启动前，boot loader会将存储介质(一般是硬盘)中的initrd文件加载到内存，内核启动时会在访问真正的根文件系统前先访问该内存中的initrd文件系统。
- /bin 该目录中存放Linux的常用命令。
- /sbin 该目录用来存放系统管理员使用的管理程序。
- /var 该目录存放那些经常被修改的文件，包括各种日志、数据文件。
- /etc 该目录存放系统管理时要用到的各种配置文件和子目录，例如网络配置文件、文件系统、X系统配置文件、设备配置信息、设置用户信息等。
- /dev 该目录包含了Linux系统中使用的所有外部设备，它实际上是访问这些外部设备的端口，访问这些外部设备与访问一个文件或一个目录没有区别。
- /mnt 临时将别的文件系统挂在该目录下。
- /root 如果你是以超级用户的身份登录的，这个就是超级用户的主目录。
- /home 如果建立一个名为“xx”的用户，那么在/home目录下就有一个对应的“/home/xx”路径，用来存放该用户的主目录。
- /usr 用户的应用程序和文件几乎都存放在该目录下。
- /lib 该目录用来存放系统动态链接共享库，几乎所有的应用程序都会用到该目录下的共享库。
- /opt 第三方软件在安装时默认会找这个目录,所以你没有安装此类软件时它是空的,但如果你一旦把它删除了,以后在安装此类软件时就有可能碰到麻烦。
- /tmp 用来存放不同程序执行时产生的临时文件，该目录会被系统自动清理干净。
- /proc 可以在该目录下获取系统信息，这些信息是在内存中由系统自己产生的，该目录的内容不在硬盘上而在内存里。
- /misc 可以让多用户堆积和临时转移自己的文件。
- /lost＋found 该目录在大多数情况下都是空的。但当突然停电、或者非正常关机后，有些文件就临时存放在这里。

### Linux文件颜色的含义：
- 蓝色为文件夹
- 绿色是可执行文件，可执行的程序
- 浅蓝色是链接文件
- 红框文件是加了SUID位，任意限权
- 红色为压缩文件或者包文件
- 褐色为设备文件
- 白色为一般性文件，如文本文件，配置文件，源码文件等

## 脚本
- run.sh
```
#!/bin/bash
echo stop application
source ./stop.sh
echo start application
source ./start.sh
```
- start.sh
```
#!/bin/bash
nohup java -jar usertask-0.5-SNAPSHOT.jar spring.profiles.active=test >./usertask.log 2>&1 &
```
- stop.sh
```
#!/bin/bash
PID=$(ps -ef | grep usertask-0.5-SNAPSHOT.jar | grep -v grep | awk '{ print $2 }')
if [ -z "$PID" ]
then
    echo Application is already stopped
else
    echo kill $PID
    kill $PID
fi
```

### Rabbitmq启动命令
```
docker stop rabbitmq3.7.7; docker rm rabbitmq3.7.7; docker run -d --name rabbitmq3.7.7 -p 5672:5672 -p 15672:15672 -v /var/log/rabbitmq:/var/log/rabbitmq -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin docker.io/rabbitmq:3.7.7-management
```
