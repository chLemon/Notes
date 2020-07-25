GitHub常见错误



# RPC failed; curl 56 OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 10054

有文件太大导致的。文件大小的缓存设置大点:

 git config --global http.postBuffer  524288000