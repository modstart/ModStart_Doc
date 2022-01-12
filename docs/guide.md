
<p align="center">
  <a href="https://modstart.com">
    <img src="https://ms-assets.modstart.com/data/image/2021/09/08/23652_1f1j_9825.png" alt="ModStart" width="360" />
  </a>
</p>
<p align="center">
  模块化的极速开发框架
</p>

<p align="center">  
  <a href="https://github.com/modstart/ModStartCMS" target="_blank">
    <img alt="License Apache2.0" src="https://img.shields.io/badge/License-Apache2.0-blue">
  </a>
  <a href="https://github.com/modstart/ModStartCMS" target="_blank">
    <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/modstart/ModStartCMS">
  </a>
  <a href="https://github.com/modstart/ModStartCMS" target="_blank">
    <img alt="GitHub last release" src="https://img.shields.io/github/v/release/modstart/ModStartCMS">
  </a>
  <br />
  <a href="https://github.com/modstart/ModStartCMS" target="_blank">
    <img alt="Laravel" src="https://img.shields.io/badge/Framework-ModStart-blue">
  </a>
  <a href="https://github.com/modstart/ModStartCMS" target="_blank">
    <img alt="Laravel" src="https://img.shields.io/badge/PHP-Laravel-red">
  </a>
  <a href="https://github.com/modstart/ModStartCMS" target="_blank">
    <img alt="Laravel" src="https://img.shields.io/badge/JS-Vue-green">
  </a>
</p>


# ModStart是基于Laravel的模块化极速开发框架


##  🔥 当前版本

最新版本 <img alt="GitHub last release" style="vertical-align:middle;height:18px;" src="https://img.shields.io/github/v/release/modstart/ModStartCMS?style=flat-square">，功能完善，模块市场丰富，欢迎交流。

QQ交流群： [467107293](https://qm.qq.com/cgi-bin/qm/qr?k=JP5GySRSCM8BUVoIGwfXF_bCe6gPajEb&jump_from=webapi)

##  💡 系统简介

`ModStart` 是一个基于 `Laravel` 模块化极速开发框架。模块市场拥有丰富的功能应用，支持后台一键快速安装，让开发者能快的实现业务功能开发。 

系统完全开源，基于 Apache 2.0 开源协议，**免费且不限制商业使用**。


<img src="https://ms-assets.modstart.com/data/image/2021/11/07/46017_dv5r_7358.jpg" alt="功能架构" />

- [官方网站](https://modstart.com)
- [在线演示](https://cms.demo.tecmz.com)
- [模块市场](https://modstart.com/store)
- [源码地址 / Gitee](https://gitee.com/modstart/ModStartCMS)
- [源码地址 / GitHub](https://github.com/modstart/ModStartCMS)

**技术栈**

- [Laravel](https://laravel.com/)
- [Vue](https://vuejs.org/)
- [Element UI](https://element.eleme.io/)
- [LayUI](https://github.com/sentsin/layui)
- [jQuery](http://jquery.com)


##  💥 系统特性

- 简洁优雅、灵活可扩展
- 后台RBAC权限管理
- 模块化开发，积木式搭建系统
- 组件按需加载静态资源
- 丰富的数据表格、数据表单功能
- 内置文件上传，无需繁琐的开发
- 丰富的模块市场，后台一键快速安装



## 🎨 系统演示

### 前台演示地址

[http://cms.demo.tecmz.com/](http://cms.demo.tecmz.com/)

> 用户密码自行注册使用

### 后台演示地址

[http://cms.demo.tecmz.com/admin](http://cms.demo.tecmz.com/admin)

> 账号：`demo` 密码：`123456` （演示账号为只读权限）



## 🎁 模块市场

丰富的模块市场，后台一键安装模块应用

![模块市场](https://ms-assets.modstart.com/data/image/2022/01/12/21242_me7h_4616.jpg)



## 🌐 开发文档

[https://modstart.com/doc](https://modstart.com/doc)


##  🔧 系统安装

### 环境要求

- `PHP` `5.6 或 7.0`
- `MySQL` `>=5.0`
- `PHP Extension`：`Fileinfo`
- `Apache/Nginx`

> 强力推荐使用PHP 5.6 或 7.0 版本，系统稳定性最好

### 安装说明

- 宝塔一键安装教程：[https://modstart.com/doc/install/baota.html](https://modstart.com/doc/install/baota.html)
- PHPStudy一键安装教程：[https://modstart.com/doc/install/phpstudy.html](https://modstart.com/doc/install/phpstudy.html)
- WampServer安装教程：[https://modstart.com/doc/install/wampserver.html](https://modstart.com/doc/install/wampserver.html)
- Docker一键安装教程：[https://modstart.com/doc/install/docker.html](https://modstart.com/doc/install/docker.html)
- 原生环境安装教程：[https://modstart.com/doc/install/start.html](https://modstart.com/doc/install/start.html)


### 升级指南

参照 [https://modstart.com/doc/install/upgrade.html](https://modstart.com/doc/install/upgrade.html)




##  🔨 开发速看


以下以一个简单的新闻增删改查页面为例，快速了解 ModStart 开发的大致流程。

### 数据表迁移文件

```php
class CreateNews extends Migration
{
    public function up()
    {
        Schema::create('news', function (Blueprint $table) {
            $table->increments('id');
            $table->timestamps();
            $table->string('title', 200)->nullable()->comment('');
            $table->string('cover', 200)->nullable()->comment('');
            $table->string('summary', 200)->nullable()->comment('');
            $table->text('content')->nullable()->comment('');
        });
    }
    public function down()
    {
        //
    }
}
```

### 控制器代码

```php
class NewsController extends Controller
{
    use HasAdminQuickCRUD;
    protected function crud(AdminCRUDBuilder $builder)
    {
        $builder
            ->init('news')
            ->field(function ($builder) {
                $builder->id('id','ID');
                $builder->text('title', '名称');
                $builder->image('cover', '封面');
                $builder->textarea('summary', '摘要');
                $builder->richHtml('content', '内容');
                $builder->display('created_at', '创建时间');
                $builder->display('updated_at', '更新时间');
            })
            ->gridFilter(function (GridFilter $filter) {
                $filter->eq('id', 'ID');
                $filter->like('title', '标题');
            })
            ->title('新闻管理');
    }
}
```

### 增加路由和导航

在 `routes.php` 增加路由信息

```php
$router->match(['get', 'post'], 'news', 'NewsController@index');
$router->match(['get', 'post'], 'news/add', 'NewsController@add');
$router->match(['get', 'post'], 'news/edit', 'NewsController@edit');
$router->match(['get', 'post'], 'news/delete', 'NewsController@delete');
$router->match(['get', 'post'], 'news/show', 'NewsController@show');
```


在 `ModuleServiceProvider.php` 中注册菜单信息

```php
AdminMenu::register(function () {
    return [
        [
            'title' => '新闻管理',
            'icon' => 'list',
            'sort' => 150,
            'url' => '\App\Admin\Controller\NewsController@index',
        ]
    ];
});
```

这样一个简单的新闻增删改查页面就开发完成了。



## 📋 常见问题

我们列举了常见问题，请查看官方标准指南

[https://modstart.com/doc/install/qa.html](https://modstart.com/doc/install/qa.html)

如有其他问题推荐使用官方讨论交流群或在线讨论

[https://modstart.com/forum](https://modstart.com/forum)
