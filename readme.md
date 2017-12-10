## php-decoder

基于 `zend_compile_string` 解密非扩展加密的PHP文件

### 编译

下载 `php-5.5.38` 源代码，打上补丁。不需要考虑可能需要的扩展，e.g mysqli 等等，直接编译即可

```
./configure --prefix=/tmp/php-decoder --disable-cgi --disable-fpm -q && make -j8
```

### 解密代码

这个程序会把所有动态 `eval/assert/create_function/...` 执行的内容直接显示在

```
./sapi/cli/php xxx.php
```

会在当前目录下依次生成 `compile.X.txt`，顺序递增，即这个程序每次编译的PHP代码内容，其中某一个就是解密的PHP代码

