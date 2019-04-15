# Windows

### 双显示显示双任务栏
- 下载[Dual Monitor Taskbar ](http://www.dijiu.com/soft/114481.htm#fileurl)
- 设置功能
> 比如显示Windows按键、可以 镜像-两个任务栏控制同一个页面，也可以设置单独控制自己显示屏页面。

### 快捷键
- 打开地址栏 `ctl+F4`

### 项目结构输出成文件树
- 只有文件夹 `tree >> D:/tree.txt`
- 文件夹和文件 `tree /f >> D:/tree.txt`

### 端口与进程
- 查看所有端口 `netstat -ano`
- 查看指定端口PID `netstat -ano|findstr "8080"`
- 查看是哪个进程或者程序占用PID `tasklist | findstr "2027"`
- 结束进程 `taskkill /f /t /im javaw.exe`