## 机器相关的命令

1.  **查看机器多少位**     
`uname -a`
2.  **安装Homebrew**
	`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  `
	* brew安装应用：  brew install maven
	* brew卸载应用：  brew uninstall maven
3. **安装Java并配置环境变量**
	`https://www.cnblogs.com/ceshi2016/p/6829279.html`
4. **修改环境配置**
```
cd ~       先到根目录      
vi .bash_profile      修改环境变量文件
source .bash_profile    使环境变量生效
```
5. **查询mac的ip地址**
`ifconfig | grep "inet " | grep -v 127.0.0.1`

6. 安装软件用的：Homebrew


## Linux相关命令
1. 查看机器上各个文件夹的大小,磁盘使用率  
`df -k`
2. 查看机器上指定文件夹中每个文件的大小  (-[a是字节展示，-h是K/G等展示](https://www.cnblogs.com/kobe8/p/3825461.html))
 `du -a`  	
3. 修改文件的权限 , （777是权限值，[具体的值含义](https://www.cnblogs.com/avril/archive/2010/03/23/1692809.html)）
`chmod 777 xxx.txt`
4. 清空文件内容  ,
`echo "" > xxx.txt `
5. 查看端口号占用
` netstat -anp`
6. 移动文件或文件夹   
`mv 原文件地址或原文件夹地址  新地址`
7. 删除文件/文件夹
	 - `rm 文件or文件夹`  
	 - 当文件夹非空时 `rm -rf 文件夹名`



##Git相关命令

1. git clone xxxx.git  “本地的存储目录”






##SVN相关命令
1. svn checkout  http://svn.xxxxx
