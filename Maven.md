# Maven的安装配置使用 
1. 下载maven 
    [官方网站](http://maven.apache.org)
    Maven是使用java开发，需要安装JDK1.6以上

2. 安装maven 
- 第一步：安装JDK1.6及以上 
- 第二步：将maven下载的压缩包进行解压缩
- 第三步：配置maven的环境变量MAVEN_HOME
- 第四步：配置maven的环境变量PATH
- 第五步：测试maven是否安装成功，在系统命令行中执行命令：mvn –v

3. 配置maven 

    > 在maven中有两个配置文件：用户配置、全局配置（默认） 
- 全局配置 :

    > 在maven安装目录的conf里面有一个settings.xml文件，这个文件就是maven的全局配置文件。该文件中配置来maven本地仓库的地址默认在系统的用户目录下的m2/repository中，该目录是本地仓库的目录。

4. Maven命令的使用 

    > Maven的命令要在pom.xml所在目录中去执行，可在pom.xml所在文件夹中按住shift右键，点击“在此处启动命令窗口” 

- 编译的命令 `mvn compile`
- 清除命令 `mvn clean` 
- 测试命令 `mvn test` 
- 打包命令  `mvn package` 
- 安装命令 `mvn install` 
- 先清空再编译 `mvn clean compile` 
- 先清空再测试 `mvn clean test`
- 先清空再测试 `mvn clean package`
- 先清空再安装 `mvn clean install`

5. pom.xml
- dependencies与dependencyManagement
> dependencies 即使在子项目中不写该依赖项，那么子项目仍然会从父项目中继承该依赖项（全部继承）。
dependencyManagement 里只是声明依赖，并不实现引入，因此子项目需要显示的声明需要用的依赖。如果不在子项目中声明依赖，是不会从父项目中继承下来的；只有在子项目中写了该依赖项，并且没有指定具体版本，才会从父项目中继承该项，并且version和scope都读取自父pom;另外如果子项目中指定了版本号，那么会使用子项目中指定的jar版本。