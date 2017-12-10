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

### 注意事项

最好在虚拟机里执行，或者配置下 `php.ini`，禁用所有敏感函数。由于我们无法知道这个脚本具体做了哪些事情，在开发机上执行，可能会带来意想不到的问题

## 写在最后

如果你在服务器上发现了这样的加密后门，你可以考虑安装基于RASP技术的服务器保护组件，比如 [OpenRASP](https://github.com/baidu/openrasp)

基于RASP技术可以很好的对抗WebShell，因为RASP不关心这个WebShell如何编写，如何加密和混淆，它只关心这个后门在做什么事情，并根据行为拦截攻击

我们会在今年年底推出PHP Beta版本，敬请期待






