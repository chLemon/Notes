千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符







# Mac安装Homebrew

## 国内安装(可用)：

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

安装fish

```
brew install fish
```

配置文件：

.config/fish/config.fish



修改默认shell，先打开终端，左上角，终端，偏好设置，通用，Shell的打开方式，命令`/usr/local/bin/fish`



