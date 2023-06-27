## I. pip & pip3

`pip --version`

**显示pip版本和路径**



`pip install --upgrade pip`

`pip3 install --upgrade pip`

**升级 pip (Linux or MacOS)**



`python -m pip install -U pip`

`python -m pip3 install -U pip`

**升级 pip (Windows)**



`pip install SomePackage`

**安装包的最新版本**



`pip install SomePackage==1.0.4`

**安装包的指定版本**



`pip install SomePackage>=1.0.4`

**安装包的最小版本**



`pip install --upgrade SomePackage`

**升级包, 可以使用 ==, >, >=, <, <= 来指定升级的版本**



`pip install -r requirements.txt`

**批量安装requirements.txt列出的包**

**requirements.txt内容如下**

```txt
flask
requests
PyYaml
pysocks
pyDes
apscheduler
```

`pip freeze > requirements.txt`

**导出requirements.txt**



`pip uninstall SomePackage`

**卸载包**



`pip search SomePackage`

**搜索包**



`pip show SomePackage`

**显示安装的包的信息**



`pip list`

**列出已安装的包**



`pip list -o`

**查看可升级的包**



`pip install -i mirror-site some-package`

**临时使用某个镜像站点安装包**

`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple Django`

**临时使用清华镜像站点安装Django**



`pip config set global.index-url mirror-site`

`pip config set install.trusted-host mirrors.aliyun.com`

**使用命令方式设置默认的镜像站点**

```powershell
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple
pip config set global.index-url http://mirrors.cloud.tencent.com/pypi/simple
pip config set global.index-url http://pypi.douban.com/simple
```



**手动设置镜像源**

**1.创建配置文件**

**Windows系统**

在%APPDATA%目录下创建pip目录，并在pip目录下创建pip.ini文件。

运行 -> %APPDATA% -> 创建pip目录 -> 创建pip.ini文件

\* 其中的%APPDATA%是映射到C:\Users\你的用户名\AppData\Roaming目录，也可以手动打开该目录

**Linux系统**

修改~/.pip/pip.conf文件，如果提示不存在，则创建文件。

**2.配置安装源信息**

在pip.ini或pip.conf文件输入安装源信息：
[global]
index-url=https://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host=mirrors.aliyun.com



**镜像源列表**

https://mirrors.aliyun.com/pypi/simple     阿里云
https://pypi.douban.com/simple            豆瓣
https://pypi.tuna.tsinghua.edu.cn/simple   清华大学
https://pypi.hustunique.com/               华中科技大学
https://pypi.mirrors.ustc.edu.cn/simple    中国科技大学
https://pypi.sdutlinux.org/                山东理工大学



`python -m venv virtual-env-name`

**创建虚拟空间**

`python -m venv venv`

**创建虚拟空间**



`& e:/2_webend_project/calc-gpt/venv/Scripts/Activate.ps1`

**手动调用powershell激活脚本, 激活虚拟空间。 若使用vs code, 可手动选择编译环境**



