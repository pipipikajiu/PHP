## 1 . php5.3之后,引入了命名空间 所以引入了composer 依赖管理工具

## 2 .前提条件:
- 1. php5.3+,开启open_ssl扩展 (到根目录中进入composer 目录, php - m 查看有没有开启open_ssl扩展);

## 3 . packagist.org(扩展库网址)
 - 1 . 使用composer下载安装依赖库:
    . composer require : 在应用程序目录下,安装指定的扩展库
    . composer.json 文件 : composer的配置文件,是当前应用程序关于composer的配置信息
    . composer 所有的扩展库目录都位于vendor目录
    . 两种方式安装依赖库(1: composer require;2: 在composer.json中直接写入)
- 2 .在php文件中使用第三方扩展库
    . 引入composer生成的自动加载文件
     require_once 'Vendor/autoload.php';(autoload.php : composer 自动生成的自动加载文件)
     .如果引入的扩展库有命名空间信息,则需要引入命名空间;例:
     use Carbon\Carbon
- 3. composer update:
    根据composer.json文件,更新(删除)当前应用程序.
- 4 .composer create-project:根据第三方扩展库,生成应用程序

## 3 . composer自动加载机制:
- 1 . PSR-4规范的自动加载机制:
    含有明命名空间的类,把类的 命名空间 与 目录结构对应起来,例:
    App\controller\msgController    APP->目录, controller->子目录

- 2 . 基于类目录的自动加载机制:
    不含命名空间的类;
- 3 . 基于函数库文件的自动加载机制:
    自动加载自定义函数

## 4 . 使用自定义的composer自动加载机制时,必须 使用命令composer dump-autoload生成自动加载文件,否则会报错.