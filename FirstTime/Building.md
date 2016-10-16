# Git、Maven、Intellij IDEA 环境搭建
<a id="Top"></a>
##目录
* [Git 环境配置](#Git 环境配置)
* [Maven 环境配置](#Maven 环境配置)
* [Intellij IDEA 环境配置](#Intellij IDEA 环境配置)

##一、<a id="Git 环境配置">Git 环境配置</a>

###1.安装  

Windows 版的 Git： 

　msysgit，包含模拟环境和 Git，只需要下载一个单独的 exe 安装程序，其他什么也不用装。 

###2.配置 host  

　需要修改 C:\Windows\System32\drivers\etc\hosts文件，并添加 " 218.58.-.- gitlab.trs.com "。 

***疑问：*** *为什么要在 host 文件中添加" "中的内容？*  
```bash
公司搭建的 git 服务器，添加后可以用本机 git 访问该 IP 地址，进行项目的管理。  
```
###3.配置 git 账户信息  

　git config --global user.name " sunm--- "，" "内为 git 用户名。  
　git config --global user.email " ponderman---@gmail.com "，" "内为 email。

###4.检查信息 

　config --global -l，显示本机 git 的用户信息。  


##二、<a id="Maven 环境配置">Maven 环境配置</a>

###1.下载、安装  

###2.配置环境变量  

使用 DOS 在本地测试 Maven 是否配置：  

　命令：mvn -v   

###3.配置在 IDEA  

菜单流程：  

　Run/Edit Configurations/+/Maven  

***疑问：*** *为什么不使用 IDEA 自带的 Maven？*
```bash
配置一些 IDEA-Maven 没有的特殊的作用，即创建 Maven 的 clean-install 组合来编译打包项目代码。
```
***疑问：*** *clean 和 install 有什么用？*
```bash
clean：让 Maven 清理 target 目录，因为 Maven 默认项目的输出目录为 target。
install：将本地工程打包，放入到Maven本地仓库中。
```
　***－疑问：*** *为什么清理 target 目录？ target 目录有什么用？*
```bash  
target 目录存放编译后的项目文件，比如 .class 等等。如果不清理 target 目录，下一步使用 install 时，不会重新编译整个工
程，而是直接将原有编译好的工程打包并安装到 Maven 本地仓库。试想，如果此时修改了源文件，但并未编译就被打包安装到 Maven 
本地仓库，那么修改的代码则不会生效。
```
　***－疑问：*** *为什么执行 install？*
```bash
Maven 在执行一个生命周期的命令时，将会执行之前的所有生命周期操作。所以，执行 install，会执行前面一系列的动作，包括 
compile，package，test 等，此时，Maven 本地仓库会得到重新编译后的新的工程，以方便其他 Moudle 通过 pom.xml 配置的依
赖引入最新工程代码。
```
***疑问：*** *为什么 IDEA-Maven 的 Maven 命令组合不好？*
```bash
IDEA-Maven 没有自带的 Maven 命令组合，只有单个命令，虽然每次都可以选择单个命令组合使用，但是使用起来不方便。
```

***注意：*** *每个项目都默认使用 IDEA 自带 Maven，每个都需要手动设置 Maven。*    


##三、<a id="Intellij IDEA 环境配置">Intellij IDEA 环境配置</a>

###1.Git 配置  

菜单路径：  

　settings/version control/git，配置 git.exe 路径。  
 
###2.GitHub 配置  

菜单路径：

　settings/version control/git hub，配置 GitHub 账户信息。  
  
　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　[返回顶部](#Top)
