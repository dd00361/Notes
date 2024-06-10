### 1. 模板继承（个人推荐）

**base.html 基础模板**

```html
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>{block name="title"}标题{/block}</title>
</head>
<body>
    {block name="menu"}菜单{/block}
    {block name="left"}左边分栏{/block}
    {block name="main"}主内容{/block}
    {block name="right"}右边分栏{/block}
    {block name="footer"}底部{/block}
</body>
</html>
```

**子模板：**

```html
{extend name="base" /}

{block name="title"}{$title}{/block}

{block name="menu"}
<a href="/" >首页</a>
<a href="/info/" >资讯</a>
<a href="/bbs/" >论坛</a>
{/block}

{block name="left"}{/block}

{block name="main"}
{volist name="list" id="vo"}
<a href="/new/{$vo.id}">{$vo.title}</a><br/>
 {$vo.content}
{/volist}
{/block}

{block name="right"}
 最新资讯：
{volist name="news" id="new"}
<a href="/new/{$new.id}">{$new.title}</a><br/>
{/volist}
{/block}

{block name="footer"}
{__block__}
 @ThinkPHP 版权所有
{/block}
```

### 2. 模板布局

**第一种方式：全局配置方式**

```php
// template.php
return  [
    'layout_on'     =>  true,
    'layout_name'   =>  'layout',
];
```

**layout.html**

```html
{include file="public/header" /}
 {__CONTENT__}
{include file="public/footer" /}
```

**第二种方式：模板标签方式**

```html
{layout name="layout" /}
```

**第三种方式：动态方法布局**

```php
namespace app\index\controller;

use think\Controller;

class User extends Controller
{
    public function add() 
    {
        $this->view->engine->layout(true);//普通用法
        //$this->view->engine->layout('Layout/newlayout');//模板位置：Layout/newlayout
        //$this->view->engine->layout(false);//临时关闭当前模板的布局功能
        return $this->fetch('add');
    }
}
```
