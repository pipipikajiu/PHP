## 1 . MVC的优势各个模块
```javascript
耦合度低
重用性高
可维护性高
有利于软件的工程化


/application/command.php : 控制台配置文件  用命令行之行thinkphp时 读取该文件
/application/common.php :  项目的公共文件 通用函数放在该文件  可以映射全局 
/application/config.php :  配置文件 所有模块通用的
/extend : 第三方类库
/vendor : 通过composer 安装的所有类库 都在该文件夹 

```
## 2 ./public/router.php 
```php
如果本地 没有安装apache或者nginx  可以通过启动该文件,启动tp自带的Web Server
启动方法:
cd public 
php -S localhost : 8888 router.php 
contro + c 退出后 服务关闭
```
## 3 . common 模块
公共模块  不允许 在URL中访问,

- 3.1 . 
    假如 common中有一个index文件
    ```php
    namespace app\common\controller
    class Index{
        public function index(){
            return 'this is common Index index';
        }
    }


    ```
    在其他模块可以调用
    ```php
    namespace app\index\controller;
    use app\common\controller\index as commonIndex;
    public function common (){
        $common  = new commonIndex();
        return $common -> index();
    }

    ```
- 3.2 . 继承
在common中写一个 User.php
```php
namespace app\common\controller;
class User{
    public function showName($name = ''){
        return "my name is {$name}";
    }

}
```

其他模块 新建User.php
```php
namespace app\index\controller;
use app\common\controller\User as commonUser;
class User extends commonUser{
    public function demo(){
        return $this->showName('lxz');
    }
}
```
## 4 . 惯例配置
/thinkphp/convention.php;


注 : 
```php
getcwd() ：显示是 在哪个文件里调用此文件 的目录

__DIR__ ：当前内容写在哪个文件就显示这个文件目录

__FILE__ ： 当前内容写在哪个文件就显示这个文件目录+文件名


config(): tp的助手函数,若不传递任何参数,将返回当前应用的所有配置;

```

## 5 . 应用配置(app)
```php
原理:
array_merge() : 把两个数组合并为一个数组：
将两个关联数组合并为一个数组时, 当遇到两个数组键相同时,后者的值会替代前者的值.
```
## 6 . 扩展配置

