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