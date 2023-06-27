## 1>相关文章 
[系统镜像下载地址](https://cn.ubuntu.com)

[VMWare虚拟机安装Ubuntu系统1](https://www.jianshu.com/p/f0e7d85fe92e)

[VMWare虚拟机安装Ubuntu系统2](https://www.jianshu.com/p/bd2545f093b5)

[Win10下安装配置使用WSL2](https://blog.csdn.net/RenLJ1895/article/details/122741040)

[windows10安装和配置terminal、WSL、putty](https://blog.csdn.net/weixin_43883625/article/details/107827982)

[Windows下安装WSL与升级WSL2的方法](https://blog.csdn.net/qq_35333978/article/details/113177819)

[在WSL中启动Ubuntu 20.04时出现错误[出现错误 2147942402 (0x80070002) (启动“ubuntu2004.exe”时)]](https://blog.csdn.net/huahuaaaaaa1/article/details/127661144)

[WSL2出现“参考的对象类型不支持尝试的操作”的解决方法](https://www.jianshu.com/p/7bd8cfbb5b01)

## 2>常用命令

### 2-1>软件操作命令

* 更新系统数据： sudo apt-get update

* 更新所有已安装的软件：sudo apt-get upgrade

* 升级系统：sudo apt-get dist-upgrade

* 安装软件： sudo apt-get install software

* 卸载软件:sudo apt-get remove software

* 卸载并清除配置：sudo apt-getremove --purge sofaware

* 自动删除长期不需要的软件: sudo apt autoremove

* 修复依赖命令: sudo apt-get-f install

* 自动安装（autoconf/automake主要用于创建Makefile）:sudo apt-get install automakeapt-cache search package 搜索包

* apt-cache show package 获取包的相关信息，如说明、大小、版本等

* sudo apt-get install package 安装包

* sudo apt-get install package –reinstall 重新安装包

* sudo apt-get -f install 强制安装

* sudo apt-get remove package 删除包

* sudo apt-get remove package –purge 删除包，包括删除配置文件等

* sudo apt-get autoremove 自动删除不需要的包

* sudo apt-get update 更新源

* sudo apt-get upgrade 更新已安装的包

* sudo apt-get dist-upgrade 升级系统

* sudo apt-get dselect-upgrade 使用 dselect 升级

* apt-cache depends package 了解使用依赖

* apt-cache rdepends package 了解某个具体的依赖

* sudo apt-get build-dep package 安装相关的编译环境

* apt-get source package 下载该包的源代码

* sudo apt-get clean && sudo apt-get autoclean 清理下载文件的存档

* sudo apt-get check 检查是否有损坏的依赖
