### 安装 Apache HTTP 服务器（简称 Apache）。以下是详细的安装步骤：

1. #### 更新软件包索引：首先，确保您的系统上的软件包索引是最新的。打开终端（快捷键：Ctrl+Alt+T）并运行以下命令：

   ```bash
   sudo apt update
   ```

2. #### 安装 Apache：安装 Apache 的方式是使用 apt 包管理器。在终端中运行以下命令安装 Apache：

   ```bash
   sudo apt install apache2
   ```

3. #### 启动 Apache：安装完成后，Apache 不会自动启动。您可以使用以下命令手动启动 Apache 服务：

   ```bash
   sudo systemctl start apache2
   ```

4. #### 设置 Apache 开机自启动：如果您希望 Apache 在系统启动时自动启动，请运行以下命令：

   ```bash
   sudo systemctl enable apache2
   ```

5. #### 检查 Apache 状态：您可以使用以下命令检查 Apache 服务器是否正在运行：

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

6. #### 设置防火墙规则（可选）：如果您启用了防火墙（例如 UFW），则需要允许 HTTP 和 HTTPS 通信。运行以下命令允许 HTTP 和 HTTPS 流量：

   ```bash
   sudo ufw allow 'Apache'
   ```

7. #### 测试 Apache：打开您的 Web 浏览器并访问 `http://localhost`。如果您看到 Apache2 默认页面，则表示 Apache 安装成功。

这样，您就成功安装并启动了 Apache 服务器。

---

### 安装Mysql。以下是详细的安装步骤：

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

   7.1.

   - 使用 root 用户登录到 MariaDB。
   - 执行以下命令以允许远程访问：

     ```sql
     CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';
     GRANT ALL PRIVILEGES ON *.* TO 'your_username'@'%' WITH GRANT OPTION;
     FLUSH PRIVILEGES;
     ```
  
     **sql讲解：**  
   
     `CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';`

     创建了一个新用户，该用户可以从任何主机（`'%'`）连接到 MySQL 服务器，并使用指定的密码进行身份验证。

     `GRANT ALL PRIVILEGES ON *.* TO 'your_username'@'%' WITH GRANT OPTION;`

     授予了该用户在所有数据库和所有表上的所有权限，并且还赋予了该用户将这些权限授予其他用户的权限（`WITH GRANT OPTION`）。

     这两个命令通常一起使用，目的是创建一个具有管理权限的用户，该用户可以从远程主机连接到 MySQL 服务器，并且可以授予其他用户权限。请注意，为了安全起见，应该仔细限制授予的权限，以确保不会授予不必要的权限给用户。

   7.2
   
   编辑/etc/mysql/mariadb.conf.d/50-server.cnf文件中bind-address = 0.0.0.0

   这一行指定了 MySQL 服务器绑定的 IP 地址。在这里，0.0.0.0 表示 MySQL 将在所有可用的网络接口上监听连接。这意味着 MySQL 将接受来自任何 IP 地址的连接请求。如果你希望 MySQL 服务器只接受特定 IP 地址的连接请求，可以将 bind-address 设置为该 IP 地址。
     
9. **防火墙配置**（可选）：如果您启用了防火墙（例如 UFW），请确保允许 MariaDB 的通信。您可以运行以下命令允许 MariaDB 流量：

   ```bash
   sudo ufw allow mysql
   ```

现在，您已经成功安装并配置了 MariaDB（MySQL）服务器。

**补充**

如果需要远程登录（例如：Navicat)需要开启服务器的TCP协议3306端口

---

### 安装 PHP 可以通过以下步骤完成。下面是详细的步骤：

1. #### 更新软件包列表

   在安装任何新软件包之前，最好先更新现有的软件包列表。这可以通过以下命令完成：
   
   ```bash
   sudo apt update
   ```

2. #### 安装 PHP

   在 Ubuntu 中，您可以使用 `apt` 包管理器来安装 PHP。默认情况下，Ubuntu 软件库中包含 PHP 7.4，这是在 Ubuntu 20.04 中的默认版本。要安装 PHP 以及一些常见的 PHP 扩展，请运行以下命令：
   
   ```bash
   sudo apt install php php-cli php-fpm php-json php-common php-mysql php-zip php-gd php-mbstring php-curl php-xml php-bcmath php-json
   ```

3. #### 验证 PHP 安装

   安装完成后，可以使用以下命令验证 PHP 是否已成功安装：
   
   ```bash
   php -v
   ```
   
   该命令将输出已安装的 PHP 版本及其相关信息。

4. #### 配置 PHP（可选）

   根据您的需求，您可能需要编辑 PHP 配置文件。PHP 的主配置文件是 `/etc/php/7.4/apache2/php.ini`（如果您使用的是 Apache）或 `/etc/php/7.4/fpm/php.ini`（如果您使用的是 PHP-FPM）。
   
   可以使用 `nano` 或任何其他文本编辑器来编辑此文件。例如：
   
   ```bash
   sudo nano /etc/php/7.4/apache2/php.ini
   ```
   
   或者
   
   ```bash
   sudo nano /etc/php/7.4/fpm/php.ini
   ```

5. #### 重启 Web 服务器

   如果您使用的是 Apache 作为 Web 服务器，请重启 Apache 以使更改生效：
   
   ```bash
   sudo systemctl restart apache2
   ```
   
   如果您使用的是 Nginx 和 PHP-FPM，请重启 PHP-FPM 和 Nginx：
   
   ```bash
   sudo systemctl restart php7.4-fpm
   sudo systemctl restart nginx
   ```

6. #### 检查 PHP 是否工作

   您可以创建一个简单的 PHP 文件来验证 PHP 是否正常工作。在您的 Web 服务器的根目录（例如 `/var/www/html`）中创建一个名为 `index.php` 的文件，并添加以下内容：
   
   ```php
   <?php
   phpinfo();
   ?>
   ```
   
   然后，在浏览器中访问 `http://your_server_ip/index.php`，您应该会看到一个显示 PHP 配置信息的页面。如果看到了这个页面，说明 PHP 已成功安装并配置。

   ---

   ### 注意事项：项目中需要确认runtime文件夹的存在

   ---
   
   ### 常见问题

      #### 1.在 HTML 页面中引用 CSS 文件出现 404 错误，通常是因为服务器找不到该文件。在基于 Ubuntu、Apache、MySQL 和 ThinkPHP 5.1 的环境中，可以按以下步骤来解决这个问题：
   
      ##### 1.1 检查文件路径
      
      确保文件 `/static/css/GoogleFont.css` 实际存在于项目目录中。检查路径是否正确，文件名是否拼写错误。
      
      ##### 1.2 检查项目目录结构
      
      确保静态文件目录结构正确，并且 Apache 可以访问该目录。假设项目目录结构如下：
      
      ```
      /path/to/your/project/
      ├── public/
      │   ├── index.php
      │   └── static/
      │       └── css/
      │           └── GoogleFont.css
      ```
      
      在这种情况下， `DocumentRoot` 应该指向 `public` 目录。
      
      ##### 1.3 检查 Apache 配置
      
      确保 Apache 配置中的 `DocumentRoot` 指向项目的 `public` 目录。编辑 Apache 配置文件（例如 `/etc/apache2/sites-available/000-default.conf`）：
      
      ```apache
      <VirtualHost *:80>
          ServerAdmin webmaster@localhost
          DocumentRoot /path/to/your/project/public
      
          <Directory /path/to/your/project/public>
              Options Indexes FollowSymLinks
              AllowOverride All
              Require all granted
          </Directory>
      
          ErrorLog ${APACHE_LOG_DIR}/error.log
          CustomLog ${APACHE_LOG_DIR}/access.log combined
      </VirtualHost>
      ```
      
      ##### 1.4 启用 `mod_rewrite`
      
      确保已启用 Apache 的 `mod_rewrite` 模块，并允许 `.htaccess` 文件生效：
      
      ```bash
      sudo a2enmod rewrite
      sudo systemctl restart apache2
      ```
      
      确保 `.htaccess` 文件在 `public` 目录中，并包含适当的重写规则。例如：
      
      ```apache
      <IfModule mod_rewrite.c>
          Options +FollowSymlinks -Multiviews
          RewriteEngine on
      
          # 静态资源重写规则
          RewriteCond %{REQUEST_FILENAME} !-f
          RewriteCond %{REQUEST_FILENAME} !-d
          RewriteRule ^(.*)$ index.php/$1 [L]
      </IfModule>
      ```
      
      ##### 1.5 检查权限
      
      确保静态文件和目录对 Apache 用户具有读取权限。运行以下命令：
      
      ```bash
      sudo chown -R www-data:www-data /path/to/your/project
      sudo chmod -R 755 /path/to/your/project
      ```
      
      ##### 1.6 清理浏览器缓存
      
      有时，浏览器可能会缓存旧的请求结果。尝试清理浏览器缓存，或者在新的隐私窗口中重新加载页面。
      
      ##### 1.7 重启 Apache 服务器
      
      在做了以上修改后，务必重启 Apache 服务器使更改生效：
      
      ```bash
      sudo systemctl restart apache2
      ```
      
      ##### 1.8 查看 Apache 错误日志
      
      如果问题仍然存在，可以查看 Apache 错误日志，以获取更多详细信息：
      
      ```bash
      sudo tail -n 50 /var/log/apache2/error.log
      ```
      
      通过上述步骤，您应该能够解决在 HTML 页面中引用 CSS 文件出现 404 错误的问题。


      #### 2.出现 SQLSTATE[HY000] [1698] Access denied for user 'root'@'localhost' 错误，表示ThinkPHP连接MySQL数据库时，使用root用户被拒绝访问。这个问题通常与MySQL用户权限配置有关。以下是解决该问题的步骤：

      确认 `root` 用户在 `localhost` 主机上有权限，如果有并将plugin字段的值改为`mysql_native_password`(即使用mysql_native_password认证插件）。
