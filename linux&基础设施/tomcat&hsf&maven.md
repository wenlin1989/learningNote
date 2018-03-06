##本地启动Tomcat

1. 准备工作：
	* 下载tomcat安装包  ---解压后得到安装包放置路径
	* 下载pandora安装包  ---解压后（后缀为.sar）得到安装包的放置路径
	* 本地创建/home/admin 的目录（用于部分资源进行线上拉取后本地放置）
		*  sudo mkdir /home/admin
		*  ls -l /home/
		*  cd home
		*  sudo chmod 777 admin

2. idea本地启动配置
	* Run - Debug Configurations - 创建一个local的tomcat Server实例
	* 对tomcat Server中的Server进行配置：
		*  Application server：选择放置tomcat解压包的地址，确定tomcat
		*  Open browser : 若不需要buc登录则直接localhost即可，若需要则改为项目的域名，并且在机器的hosts中将域名的ip配置为127.0.0.1  
		*  VM options：此处需要进行启动参数配置
			* -Dantx.properties=antx.properties文件的绝对路径
			* -Dpandora.location= sar包解压后的绝对路径
			* 其他需要配置的参数也可以在此进行配置
	* 对tomcat中的Deployment进行配置 :
		* 选择需要打成war包的工程进行编译（选择exploded模式） 
			*  不带exploded的war（发布模式，达成war再发布） —— 将WEB工程以包的形式上传到服务器
			*  带exploded的war（支持热部署，将所有资源移到tomcat部署文件夹里面进行加载部署） —— 将WEB工程以当前文件夹的位置关系上传到服务器
	* 对所有的配置进行apply。然后运行Run 或者 Debug 即可在console中查看启动进度

3. 可能存在的坑
	*  build工程时outOfMemory 
		* 解决方案：调整maven运行时的内存占用大小 
			* mac：在 bash_profile环境变量配置文件中，增加以下配置 `export MAVEN_OPTS="-Xmx1024M -Xss128M -XX:MaxPermSize=1024M -XX:+CMSClassUnloadingEnabled"
` 
	* mvn install 一直存在一些莫名其妙的错误
		* 解决方案：更新maven版本到maven 2.x 不要用maven 3.x 
	
