```markdown
# Memcache 安装与配置指南

## 1. 下载 Memcache
官网上并未提供 Memcached 的 Windows 平台安装包，此下载链接源于非官方：[Memcached 1.4.5 (amd64)](http://static.jyshare.com/download/memcached-1.4.5-amd64.zip)

## 2. 下载 ThinkPHP5.1 支持的 Memcache 扩展
1. 根据 PHP 版本、NTS 以及 Zend Extension Build 和 PHP Extension Build 参数下载对应的文件：
   [Memcache 扩展](https://windows.php.net/downloads/pecl/releases/memcache/4.0.5.2/php_memcache-4.0.5.2-7.3-nts-vc15-x64.zip)

2. 将下载后的 `php_memcache.dll` 文件移动到 PHP 版本对应的 `ext` 文件夹中。

3. 在 PHP 版本对应的 `php.ini` 文件的 Dynamic Extensions 部分添加：
   ```ini
   extension=php_memcache
   ```

4. 通过 `phpinfo` 命令查看扩展是否正确加载。

## 3. 建议
建议将上述 1. 和 2. 两个文件放在名为 `memcache` 文件夹中，然后放在 WAMP 环境中的 `Extension` 文件夹中。（此点非必须）

## 4. 修改 ThinkPHP5.1 中 `cache.php` 代码
```php
<?php
// +----------------------------------------------------------------------
// | 缓存设置
// +----------------------------------------------------------------------

return [
    // 驱动方式
    'type'   => 'memcache',
    // host 和 port 来源于 E:\phpStudy\phpStudy_64\WWW\tp51.com\thinkphp\library\think\cache\driver\Memcache.php 中的 options 参数中。
    'host'   => '127.0.0.1',
    'port'   => 11211,
    // 缓存保存目录
    'path'   => '',
    // 缓存前缀
    'prefix' => '',
    // 缓存有效期 0 表示永久缓存
    'expire' => 0,
];
```

## 5. 完成
现在可以使用！
```
