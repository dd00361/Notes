**安装 Apache HTTP 服务器（简称 Apache）。以下是详细的安装步骤：**

1. **更新软件包索引**：首先，确保您的系统上的软件包索引是最新的。打开终端（快捷键：Ctrl+Alt+T）并运行以下命令：

   ```bash
   sudo apt update
   ```

2. **安装 Apache**：安装 Apache 的方式是使用 apt 包管理器。在终端中运行以下命令安装 Apache：

   ```bash
   sudo apt install apache2
   ```

3. **启动 Apache**：安装完成后，Apache 不会自动启动。您可以使用以下命令手动启动 Apache 服务：

   ```bash
   sudo systemctl start apache2
   ```

4. **设置 Apache 开机自启动**：如果您希望 Apache 在系统启动时自动启动，请运行以下命令：

   ```bash
   sudo systemctl enable apache2
   ```

5. **检查 Apache 状态**：您可以使用以下命令检查 Apache 服务器是否正在运行：

   ```bash
   sudo systemctl status apache2
   ```

   如果 Apache 正在运行，您将看到类似以下内容的输出：

   ```
   ● apache2.service - The Apache HTTP Server
      Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
      Active: active (running) since Tue 2024-06-11 08:00:00 UTC; 10min ago
      ...
   ```

6. **设置防火墙规则**（可选）：如果您启用了防火墙（例如 UFW），则需要允许 HTTP 和 HTTPS 通信。运行以下命令允许 HTTP 和 HTTPS 流量：

   ```bash
   sudo ufw allow 'Apache'
   ```

7. **测试 Apache**：打开您的 Web 浏览器并访问 `http://localhost`。如果您看到 Apache2 默认页面，则表示 Apache 安装成功。

这样，您就成功安装并启动了 Apache 服务器。

---

**安装Mysql**

1. **更新软件包索引**：首先，确保您的系统上的软件包索引是最新的。打开终端（快捷键：Ctrl+Alt+T）并运行以下命令：

   ```bash
   sudo apt update
   ```

2. **安装 MySQL 服务器**：在 Ubuntu 20.04 中，MySQL 被替代为 MariaDB，因此您可以通过以下命令安装 MariaDB（MariaDB 是与 MySQL 兼容的数据库服务器）：

   ```bash
   sudo apt install mariadb-server
   ```

3. **启动 MariaDB 服务**：安装完成后，MariaDB 不会自动启动。您可以使用以下命令手动启动 MariaDB 服务：

   ```bash
   sudo systemctl start mariadb
   ```

4. **设置 MariaDB 开机自启动**：如果您希望 MariaDB 在系统启动时自动启动，请运行以下命令：

   ```bash
   sudo systemctl enable mariadb
   ```

5. **运行安全性脚本**：运行以下命令来增强 MariaDB 的安全性并设置 root 密码：

   ```bash
   sudo mysql_secure_installation
   ```

   按照提示操作，您可以选择设置 root 密码、删除匿名用户、禁用远程 root 登录等。

6. **测试 MariaDB 连接**：使用以下命令测试是否可以通过 root 用户登录到 MariaDB：

   ```bash
   sudo mysql -u root -p
   ```

   输入您在第 5 步中设置的 root 密码。如果成功登录，您将看到 MariaDB 提示符。

7. **设置远程访问**（可选）：默认情况下，MariaDB 只允许本地连接。如果需要远程访问，请执行以下步骤：

   - 使用 root 用户登录到 MariaDB。
   - 执行以下命令以允许远程访问：

     ```sql
     GRANT ALL ON *.* TO 'root'@'%' IDENTIFIED BY 'your_password' WITH GRANT OPTION;
     FLUSH PRIVILEGES;
     ```

     将 `'your_password'` 替换为您希望使用的密码。注意，这会在安全性上有所降低，请谨慎使用。

8. **防火墙配置**（可选）：如果您启用了防火墙（例如 UFW），请确保允许 MariaDB 的通信。您可以运行以下命令允许 MariaDB 流量：

   ```bash
   sudo ufw allow mysql
   ```

现在，您已经成功安装并配置了 MariaDB（MySQL）服务器。

---

**补充**

如果需要远程登录（例如：Navicat)需要开启服务器的TCP协议3306端口

---

**常见问题**

问题：
root@dd0036:~# sudo mysql -u root -p
Enter password: 
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)

解决：
这个错误通常表示 MySQL 拒绝了使用给定密码登录的尝试。有几种方法可以解决这个问题：

1. **确认密码正确性：** 确保你输入的密码是正确的，注意 MySQL 密码区分大小写。

2. **重置 root 密码：** 如果你忘记了 root 用户的密码，可以尝试重置密码。首先，停止 MySQL 服务：

   ```bash
   sudo systemctl stop mysql
   ```

   然后以跳过授权表的方式启动 MySQL：

   ```bash
   sudo mysqld_safe --skip-grant-tables &
   ```

   连接到 MySQL：

   ```bash
   mysql -u root
   ```

   然后在 MySQL 中执行以下命令来重置 root 密码：

   ```sql
   USE mysql;
   UPDATE user SET authentication_string=PASSWORD('new_password') WHERE User='root';
   FLUSH PRIVILEGES;
   ```

   替换 `new_password` 为你要设置的新密码。重置密码后，退出 MySQL 并重启 MySQL 服务：

   ```bash
   sudo systemctl restart mysql
   ```

3. **检查是否有其他问题：** 如果以上方法都无法解决问题，请检查系统和 MySQL 的日志文件，查看是否有其他错误信息。
