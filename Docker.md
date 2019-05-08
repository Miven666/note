# Docker

[docker文档](https://docs.docker.com/)

## 安装Docker CE

- [yum安装](https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository)
- [rpm安装](https://docs.docker.com/install/linux/docker-ce/centos/#install-from-a-package)
- [脚本安装](https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-convenience-script)

## 启动关闭
- 启动 `systemctl start docker`
- 守护进程重启 `sudo systemctl daemon-reload`
- 重启 ` systemctl restart docker`
- 重启 `sudo service docker restart`
- 关闭`systemctl stop docker`
- 关闭 `service docker stop`