# shell
## shell变量
### 定义变量
等号两边不能有空格，第二次赋值也是一样的，不加$
### 使用一个定义过的变量
前面加$
变量名外可以加{}来括起来
### 只读变量
readonly声明一下
### 删除变量
unset
### 获取字符串长度
    string="abcd"
    echo ${#string}
### 提取子字符串
    echo ${string:1:4}
提取从第2个字符开始的4个字符
### 查找子字符串
    echo `expr index "$string" io`
## shell数组
只能有1维数组，大小无限
### 定义数组
圆括号括起来，空格隔开；或者array[0]=value这样一个个赋值
### 读取数组
${array[0]}
0换成@表示获取全部元素
### 获取数组长度
    length=${#array[@]}   #或者将@换为*

## 多行注释
    :<<!
    1
    2
    3
    !
！可以换成EOF或''
## 传参
$n
$# 传进来参数的个数
$* 以一个单字符串显示所有参数，参数用空格隔开
$$ 当前进程ID
$! 后台运行的最后一个进程的ID
$@ 所有传进来的参数，但是每个参数都会用引号隔开
$- 显示shell使用的当前选项
$? 显示命令的退出状态，0表示没有错误