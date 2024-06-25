# 1.安装和配置xdebug

打开phpinfo()页面，将页面源代码复制到[https://xdebug.org/wizard](https://xdebug.org/wizard)页面中的框里，再点击"Analyse my phpinfo() output"，下载推荐的xdebug版本。

将下载的dll文件重命名为“xdebug.dll”，并放在php对应版本(当前使用版本)中的ext文件夹中(例如：`E:\phpStudy\phpStudy_64\Extensions\php\php7.3.4nts\ext`)。

重启apache服务器。

检查phpinfo页面中是否已成功出现xdebug模块。

配置xdebug：修改php对应版本的php.ini文件中[xdebug]部分相应代码：

```
[Xdebug]
zend_extension=E:/phpStudy/phpStudy_64/Extensions/php/php7.3.4nts/ext/php_xdebug.dll
;启动调试
xdebug.mode=debug
;客户端主机名或 IP 地址
xdebug.client_host=127.0.0.1
;客户端端口号
xdebug.client_port=9003
;自动启动
xdebug.start_with_request=yes
```

# 2.配置PHPStorm:

打开菜单栏文件---设置---PHP---调试，设置页面中Xdebug的“调试端口“为上述php.ini中xdebug的客户端端口号。如图：

![image-20240625023711720](https://github.com/dd00361/Notes/assets/154615217/985f899a-cf13-4ef9-a875-ea6bc8b30e3d)

打开菜单栏文件---设置---PHP---调试，点击“预配置”中的“验证”，填写“创建验证脚本的路径”为本地项目入口文件夹，例如：`E:\phpStudy\phpStudy_64\WWW\www.library.com\public`，并填写“验证脚本的URL”为本地项目的url地址加端口号，例如`http://127.0.0.1:8087`，最后点击下方“验证”。如图所示则成功配置完成：

![image](https://github.com/dd00361/Notes/assets/154615217/7b6f7b8f-f2e0-45c7-be8e-a095974e06d1)


# 3.编辑vhost.conf文件，添加“FcgidIOTimeout 3600”，如图所示。

此行代码作用是定义了FastCGI进程在与Apache进行数据交换（读取请求或写入响应）时的最大等待时间，此处定义为3600秒，即1个小时。如果不添加此行代码，则调试时会发生短时间内自动断开调试的情况，原因是进程管理器中有个超时设置,超过时间就会终止掉php进程。

![image](https://github.com/dd00361/Notes/assets/154615217/59ad3186-00d4-4266-a786-cb2e673b2a24)


# 4.使用xdebug进行断点调试：

按图1---图2---图3---图4---图5顺序进行业务调试：

点击“开始侦听PHP调试连接”，如图1:
![image](https://github.com/dd00361/Notes/assets/154615217/370ccdbe-6e4f-4af3-883b-45af704b9138)

进行业务处理，如图2：
![image](https://github.com/dd00361/Notes/assets/154615217/55b8bd8f-168b-4c44-bfe0-38d91c0c9902)

点击“来自Xdebug的传入连接”页面中的“应用更改”，如图3：
![image](https://github.com/dd00361/Notes/assets/154615217/85b68b9d-a929-418b-bf6d-45746d2aed38)

可以在需要调试的php文件的相应代码行右键点击“运行到光标处”，使调试从光标处开始。如图4：
![image](https://github.com/dd00361/Notes/assets/154615217/cc01dc60-94a5-4cd6-afd7-d4cf0ce23e8f)

可以点击下图中的“步过”按钮依序查看每一行代码的调试结果，如图5：
![image](https://github.com/dd00361/Notes/assets/154615217/45fff0fd-28e5-4ab5-b2a6-371ca76f6140)

当调试完成后别忘记点击右上方的”停止“按钮并点击“关闭侦听PHP调试连接”。
