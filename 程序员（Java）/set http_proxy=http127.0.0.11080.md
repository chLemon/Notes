set http_proxy=http://127.0.0.1:1080 

set https_proxy=127.0.0.1:1080



取消代理：
set http_proxy=
然后回车，即等号后面什么都不写

查看代理：
set http_proxy
然后回车，即不加等号，查询亲测无用







设置代理， bypass-list的参数是不走代理地址：

```
netsh winhttp set proxy proxy-server="socks=localhost:9090" bypass-list="localhost"
```

　查看当前的代理：

```
netsh winhttp show proxy
```

　　删除所有配置的代理，并直接连接网络

```
netsh winhttp reset proxy
```







github代理



1.首先第一步前提是已经打开了SS代理。

2.如果要设置全局代理，可以依照这样设置

```text
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
```

**但同时，也请注意，这里指的是https协议，也就是**

```text
git clone https://www.github.com/xxxx/xxxx.git
```

这种

对于SSH协议，也就是

```text
git clone git@github.com:xxxxxx/xxxxxx.git
```



**4.以上为总结，但我不推荐直接用全局代理**

因为如果挂了全局代理，这样如果需要克隆coding之类的国内仓库，会奇慢无比

所以我建议使用这条命令，只对github进行代理，对国内的仓库不影响

```text
git config --global http.https://github.com.proxy https://127.0.0.1:1080
git config --global https.https://github.com.proxy https://127.0.0.1:1080
```

同时，如果在输入这条命令之前，已经输入全局代理的话，可以输入进行取消

```text
git config --global --unset http.proxy
git config --global --unset https.proxy
```



socks5：



git config --global http.https://github.com.proxy socks5://127.0.0.1:1086 git config --global https.https://github.com.proxy socks5://127.0.0.1:1086 

