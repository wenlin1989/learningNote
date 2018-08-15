## 本地启动Tomcat

1.  准备工作：

    -   下载tomcat安装包  ---解压后得到安装包放置路径
    -   下载pandora安装包  ---解压后（后缀为.sar）得到安装包的放置路径
    -   本地创建/home/admin 的目录（用于部分资源进行线上拉取后本地放置）
        		_  sudo mkdir /home/admin
        		_  ls -l /home/
        		_  cd home
        		_  sudo chmod 777 admin

2.  idea本地启动配置

    -   Run - Debug Configurations - 创建一个local的tomcat Server实例
    -   对tomcat Server中的Server进行配置：
        		_  Application server：选择放置tomcat解压包的地址，确定tomcat
        		_  Open browser : 若不需要buc登录则直接localhost即可，若需要则改为项目的域名，并且在机器的hosts中将域名的ip配置为127.0.0.1
        		_  VM options：此处需要进行启动参数配置
        			_ -Dantx.properties=antx.properties文件的绝对路径
        			_ -Dpandora.location= sar包解压后的绝对路径
        			_ 其他需要配置的参数也可以在此进行配置
    -   对tomcat中的Deployment进行配置 :
        		_ 选择需要打成war包的工程进行编译（选择exploded模式）
        			_  不带exploded的war（发布模式，达成war再发布） —— 将WEB工程以包的形式上传到服务器
        			\*  带exploded的war（支持热部署，将所有资源移到tomcat部署文件夹里面进行加载部署） —— 将WEB工程以当前文件夹的位置关系上传到服务器
    -   对所有的配置进行apply。然后运行Run 或者 Debug 即可在console中查看启动进度

3.  可能存在的坑
    	_  build工程时outOfMemory
    		_ 解决方案：调整maven运行时的内存占用大小
    			_ mac：在 bash_profile环境变量配置文件中，增加以下配置 `export MAVEN_OPTS="-Xmx1024M -Xss128M -XX:MaxPermSize=1024M -XX:+CMSClassUnloadingEnabled"`
    	_ mvn install 一直存在一些莫名其妙的错误
    		\* 解决方案：更新maven版本到maven 2.x 不要用maven 3.x

## maven

1.  命令行输入以下命令，创建一个示例工程：
    `mvn archetype:generate -B -DarchetypeGroupId=com.taobao.itest.archetypes
    -DarchetypeArtifactId=itest-service-sample-archetype
    -DarchetypeVersion=1.3-SNAPSHOT
    -DarchetypeRepository=http://mvnrepo.taobao.ali.com/mvn/snapshots-DgroupId=com.taobao.qatest
    -DartifactId=mytestproject`
2.  Maven安装成功后，其根目录下的文件结构：

-   bin：该目录包含了mvn 运行的脚本，这些脚本用来配置Java 命令，准备好classpath 和相关的Java 系统属性，然后执行Java 命令。
-   boot： 该目录只包含一个文件，这是一个类加载器框架，提供了更丰富的语法以方便配置，Maven使用该框架加载自己的类库。一个负责创建maven运行所需要的类装载器的JAR文件（classwords.jar）
-   conf： 该目录包含了一个非常重要的文件settings.xml。
-   LICENSE.txt 记录了Maven 使用的软件许可证。
-   NOTICE.txt 记录了Maven 包含的第三方软件,一些maven依赖的类库所需要的通告及权限
-   README.txt 包含了Maven 的简要介绍，一些安装指令
-   lib：有一个包含maven核心的jar文件（maven-x.x.x-uber.jar）

3.  Maven配置文件：

-   ：$M2_HOME/conf/settings.xml是全局范围的配置文件，会影响到整个机器上的所有用户
-   ~/.m2/settings.xml是用户范围的配置文件，只有当前用户才会受到该配置的影响。
-   setting.xml:
    -   localRepository：表示本地库的保存位置，也就是maven2主要的jar保存位置
    -   offline：如果不想每次编译，都去查找远程中心库，那就设置为true。当然前提是你已经下载了必须的依赖包
    -   Mirrors :表示镜像库，指定库的镜像，用于增加其他库
    -   Profiles  类似于pom.xml中的profile元素，主要包括activation,repositories,pluginRepositories 和properties元素,就是个性化配置。
        -   单独定义profile后，并不会生效，需要通过满足条件来激活
        -   repositories 和pluginRepositories 定义其他开发库和插件开发库。
    -   Activation :用于激活此profile
