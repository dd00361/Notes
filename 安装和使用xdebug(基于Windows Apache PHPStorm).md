# 1.安装和配置xdebug

打开phpinfo()页面，将页面源代码复制到https://xdebug.org/wizard页面中的框里，再点击"Analyse my phpinfo() output"，下载推荐的xdebug版本。

将下载的dll文件重命名为"xdebug.dll"，并放在php对应版本(当前使用版本)中的ext文件夹中(例如：E:\phpStudy\phpStudy_64\Extensions\php\php7.3.4nts\ext)。

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

![image-20240625023711720](C:\Users\dd003\AppData\Roaming\Typora\typora-user-images\image-20240625023711720.png)

打开菜单栏文件---设置---PHP---调试，点击”预配置“中的”验证“，填写”创建验证脚本的路径“为本地项目入口文件夹，例如E:\phpStudy\phpStudy_64\WWW\www.library.com\public，并填写”验证脚本的URL“为本地项目的url地址加端口号，例如http://127.0.0.1:8087，最后点击下方”验证“。如图所示则成功配置完成：

![image-20240625022607520](C:\Users\dd003\AppData\Roaming\Typora\typora-user-images\image-20240625022607520.png)

# 3.使用xdebug进行断点调试：

点击phpstorm界面右上角的“开始侦听PHP调试连接”，如图：![image-20240625022759199](C:\Users\dd003\AppData\Roaming\Typora\typora-user-images\image-20240625022759199.png)

进行业务调试：

在图1中点击“保存”后，进行图2所示：

![image-20240625023033911](C:\Users\dd003\AppData\Roaming\Typora\typora-user-images\image-20240625023033911.png)图1

![image-20240625023012076](C:\Users\dd003\AppData\Roaming\Typora\typora-user-images\image-20240625023012076.png)图2

可以点击下图中的按钮查看每一行代码的执行结果：
![image-20240625023329822](C:\Users\dd003\AppData\Roaming\Typora\typora-user-images\image-20240625023329822.png)

当调试完成后别忘记点击右上方的”停止“按钮并点击“关闭侦听PHP调试连接”。