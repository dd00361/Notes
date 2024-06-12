要彻底删除 `httpd` 服务及其相关文件，您可以按照以下步骤操作：

### 1. 停止 httpd 服务

首先，停止正在运行的 `httpd` 服务：

```bash
sudo systemctl stop httpd
```

### 2. 卸载 httpd 软件包

使用 `yum` 卸载 `httpd` 软件包及其依赖项：

```bash
sudo yum remove httpd
```

### 3. 删除配置文件和日志文件

删除 `httpd` 的配置文件和日志文件：

```bash
sudo rm -rf /etc/httpd
sudo rm -rf /var/log/httpd
```

### 4. 清理 httpd 的数据目录

如果 `httpd` 使用了数据目录（如网站文件），也要将其清理掉：

```bash
sudo rm -rf /var/www/html
```

### 5. 清理系统服务配置

清理 `httpd` 在系统服务中的配置信息：

```bash
sudo rm /etc/systemd/system/httpd.service
```

### 6. 更新系统并重启

更新系统的软件包信息并重启系统以确保所有更改生效：

```bash
sudo reboot
```

这样就可以彻底删除 `httpd` 服务及其相关文件。请注意，在执行上述操作之前，请确保您不再需要这些文件，并且要小心，以免删除错误的文件。
