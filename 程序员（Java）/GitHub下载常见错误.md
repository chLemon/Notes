GitHub常见错误



# RPC failed; curl 56 OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 10054

有文件太大导致的。文件大小的缓存设置大点:

 git config --global http.postBuffer  524288000



1. warning: LF will be replaced by CRLF in ball_pool/assets/Main.js.
2. The file will have its original line endings in your working directory

## 问题描述：

​     git add：添加至暂存区，但并未提交至服务器。git add . 是表示把当前目录下的所有更新添加至暂存区。有时在终端操作这个会提示：



原因：
         这是因为文件中换行符的差别导致的。这个提示的意思是说：会把windows格式（CRLF（也就是回车换行））转换成Unix格式（LF），这些是转换文件格式的警告，不影响使用。

git默认支持LF。windows commit代码时git会把CRLF转LF，update代码时LF换CRLF。
————————————————
版权声明：本文为CSDN博主「大扬哥」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_37521610/article/details/88327286

## 解决方法：

**注： . 为文件路径名**

```
git rm -r --cached .



git config core.autocrlf false



git add .



git commit -m ''



 



git push
```