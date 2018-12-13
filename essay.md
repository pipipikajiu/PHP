##1 . 乱码问题
```php
iconv("UTF-8","gbk",$new);(linux上需安装libiconv才支持iconv函数)

php页面为utf编码 
header("Content-type: text/html; charset=utf-8"); 

php页面为gbk编码 
header("Content-type: text/html; charset=gb2312"); 

```
##2 . php更改文件名称
```php
rename('oldfilename','newfilename')
```
##4 . php对象转数组
```php
$array = get_object_vars($obj);
```
##5 . yii header下载文件
```php
public function actionImages() {
        $path = User::get_url();
        $filename = $path["path"];
//        var_dump($filename);die();
        $out_filename = $path["name"];
        if( ! file_exists($filename)){
            echo 'Not Fond';exit();
        } else {
            header('Accept-Ranges:bytes');
            header('Accept-Length:'.filesize($filename));
            header('Content-Transfer-Encoding:binary');
            header('Content-type:application/octet-stream');
            header('Content-Disposition: attachment; filename='.$out_filename);
            header('Content-Type: application/octet-stream;name='.$out_filename);
            if(is_file($filename) && is_readable($filename)){
                $file = fopen($filename,'r');
                echo fread($file,filesize($filename));
                fclose($file);
            }
        }
```
## 6 . HTML中设置多个class属性的优先级
```php
css样式的优先级 是在加载css文件的时候就确定下来的,和后来html里class属性位置前后无关。

```
## 7 . yii打印最后一条sql
```php
echo $query->createCommand()->getRawSql()
```
## 8 . php.ini修改php上传文件大小限制
```php
打开php.ini，首先找到
file_uploads = on ;是否允许通过HTTP上传文件的开关。默认为ON即是开
upload_tmp_dir ;文件上传至服务器上存储临时文件的地方，如果没指定就会用系统默认的临时文件夹
upload_max_filesize = 8m ;望文生意，即允许上传文件大小的最大值。默认为2M
post_max_size = 8m ;指通过表单POST给PHP的所能接收的最大值，包括表单里的所有值。默认为8M
一般地，设置好上述四个参数后，上传<=8M的文件是不成问题，在网络正常的情况下。
但如果要上传>8M的大体积文件，只设置上述四项还一定能行的通。

进一步配置以下的参数
max_execution_time = 600 ;每个PHP页面运行的最大时间值(秒)，默认30秒
max_input_time = 600 ;每个PHP页面接收数据所需的最大时间，默认60秒
memory_limit = 8m ;每个PHP页面所吃掉的最大内存，默认8M
把上述参数修改后，在网络所允许的正常情况下，就可以上传大体积文件了
max_execution_time = 600
max_input_time = 600
memory_limit = 32m
file_uploads = on
upload_tmp_dir = /tmp
upload_max_filesize = 32m
post_max_size = 32m

```

## 9 . yii2.0 goback跳转问题
```php
goback()要先设置一下返回地址,代码:
 Yii::$app->user->setReturnUrl(Yii::$app->request->referrer); 
```
## 10 . 提取链接中的数字
```php
function findNum($str=''){
        $str=trim($str);
        if(empty($str)){return '';}
        $temp=array('1','2','3','4','5','6','7','8','9','0');
        $result='';
        for($i=0;$i<strlen($str);$i++){
            if(in_array($str[$i],$temp)){
                $result.=$str[$i];
            }
        }
        return $result;
    }
```