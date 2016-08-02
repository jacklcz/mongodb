# MongoDB 安装和命令行使用

# **window平台**

[http:\/\/www.mongodb.org\/downloads](http://www.mongodb.org/downloads "官网下载地址")

## **解压**

下载zip包后，解压安装包，并安装它。

**创建数据目录**

MongoDB将数据目录存储在 \*\*\/data\/db 目录下。但是这个数据目录不会主动创建，我们在安装完成后创建它。在根目录下（\(如： C:\ 或者 D:\ 等 \)。

## **命令行下运行 MongoDB 服务器**

从MongoDB目录的bin目录中执行mongod.exe文件。

# **MAC平台 **

使用brew install mongodb 或者官网下载 [http:\/\/www.mongodb.org\/downloads](http://www.mongodb.org/downloads "官网下载地址") ，配置环境变量即可。

![](/assets/BC304E0F-6B34-44AE-A86A-759D7972C49C.png)

# **启动**

**mongod &**

![](/assets/EF3FF6FD-97DC-4AC4-BE59-466565183F7C.png)

**mongodb启动的参数说明：**

| **参数描述** |  |
| :--- | :--- |
| --bind\_ip | 绑定服务IP，若绑定127.0.0.1，则只能本机访问，不指定默认本地所有IP |
| --logpath | 定MongoDB日志文件，注意是指定文件不是目录 |
| --logappend | 使用追加的方式写日志 |
| --dbpath | 指定数据库路径 |
| --port | 指定服务端口号，默认端口27017 |
| --serviceName | 指定服务名称 |
| --serviceDisplayNam | 指定服务名称，有多个mongodb服务时执行。dsf |







## **MongoDB后台管理 Shell**

MongoDB Shell是MongoDB自带的交互式Javascript shell,用来对MongoDB进行操作和管理的交互式环境。

当你进入mongoDB后台后，它默认会链接到 test 文档（数据库）：

![](/assets/756B8358-6788-4A8B-8D0A-4DBF1B5C40A9.png)

