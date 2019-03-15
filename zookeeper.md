# ZooKeeper

Zookeeper是Apacahe Hadoop的子项目，是一个树型的目录服务，支持变更推送，适合作为Dubbo服务的注册中心，工业强度较高，可用于生产环境，并推荐使用。

1. 可以作为集群的管理工具使用。
2. 可以集中管理配置文件。

注册中心负责服务地址的注册与查找，相当于目录服务，服务提供者和消费者只在启动时与注册中心交互，注册中心不转发请求，压力较小。

[官方下载地址](http://zookeeper.apache.org/releases.html#download)

### Zookeeper的安装
- 安装环境：
    - Linux：CentOS
    - JDK:1.7以上版本

    Zookeeper是Java开发的可以运行在windows、linux环境。需要先安装JDK。
    安装步骤：

- 第一步：安装jdk

- 第二步：把zookeeper的压缩包上传到linux系统。

- 第三步：解压缩压缩包 `tar -zxvf zookeeper-3.4.6.tar.gz`

- 第四步：进入zookeeper-3.4.6目录，创建data文件夹。

- 第五步：把zoo_sample.cfg改名为zoo.cfg `[root@localhost conf]# mv zoo_sample.cfg zoo.cfg`

- 第六步：修改data属性：dataDir=/root/zookeeper-3.4.6/data

- 第七步：启动zookeeper `[root@localhost bin]# ./zkServer.sh start`
    - 关闭：`[root@localhost bin]# ./zkServer.sh stop`
    - 查看状态：`[root@localhost bin]# ./zkServer.sh status`

- 注意：需要关闭服务器防火墙

    `systemctl stop firewalld.service #停止firewall`

    `systemctl disable firewalld.service #禁止firewall开机启动`

### 日志输出到指定文件夹

- 修改log4j.properties

  ```shell
  # 修改控制台输出为 滚动策略
  zookeeper.root.logger=INFO,ROLLINGFILE
  # 按日滚动
  log4j.appender.ROLLINGFILE=org.apache.log4j.DailyRollingFileAppender
  # 取消满10MB才滚动的策略
  #log4j.appender.ROLLINGFILE.MaxFileSize=10MB
  ```

- 修改zkEnv.sh

  ```shell
  then
      ZOO_LOG_DIR="/var/log/zookeeper"
  fi
  then
      ZOO_LOG4J_PROP="INFO,ROLLINGFILE"
  fi
  ```

- 修改zkServer.sh

  ```shell
  # 消除zookeeper.out
  _ZOO_DAEMON_OUT="$ZOO_LOG_DIR/zookeeper.log"
  ```