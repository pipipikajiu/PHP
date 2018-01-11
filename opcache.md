## opcache
   - 1 .PHP 5.5+版本以上的，可以使用PHP自带的opcache开启性能加速（默认是关闭的）。
   - 2. PHP开启opcache方法:
        1、打开php.ini文件
        2、找到：[opcache].
    - 3 . Cache hits(高级缓存命中) 
          Cache misses(高级缓存未命中)
          开启之后,源码被缓存, 不再解析php文件, 可设置: opcache.force_restart_timeout=180 控制更新速度.