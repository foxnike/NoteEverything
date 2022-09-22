# Bash
**[参考链接](https://wangdoc.com/bash/)**
>只包含部分内容，详细请参考上面链接
## 1. echo命令
>后续学习的基础 （如c语言中的printf）
``` bash
echo hello,world;
echo "hello
      world!"; #可输出多行双引号内的内容
echo -n message #取消换行
echo -e  "Hello\nWorld" #双引号内的转义符不会自动转义 -e可以解释双引号内的转义字符
```
## 2. 命令格式

```bash
command -arg1 arg2...
#一般带有配置属性的参数会在参数前有一个或两个连词符
command arg1 \
arg2；
#使用 '\' 标记一个命令未结束 方便阅读和编辑 使用';'作为命令的结束

#命令组合
command1 && command2 #命令1成功则运行命令2
command1 || command2 #命令1失败则运行命令2
```
## 3. 模式扩展
>模式扩展是bash拿到命令后，先进行扩展再执行命令（无法扩展的不进行扩展）
```bash
#类正则表达式
# ~
cd ~
cd ~root
#单独一个~会扩展为当前用户的主目录 或进入参数用户目录 没有相应用户则不会扩展
cd ~+ #扩展为当前目录
# ？ 
data? #用于匹配一位字符补全
# * 
cd data* #相当于匹配任意位字符
cd *  #匹配所有当前目录下的文件 不包含隐藏文件
cd .* #匹配所有当前目录下的文件 包含隐藏文件
# []
cd [ad].txt #匹配a.txt b.txt 
cd [a-d].txt #匹配a.txt b.txt c.txt d.txt
# ! 否定
cd a[!b-z].txt # 匹配aa.txt 除了其他a*.txt
# {} 优先级较高
cd a{b,c}.txt #匹配ab.txt ac.txt 内部元素间不能存在空格 
cd {a..c}.txt #匹配a.txt b.txt c.txt
for i in {1..4}
# $
#将$开头的词视为变量
echo $shell 
echo ${shell}
echo ${!S*} #返回满足S*的所有变量名
echo $(command) #返回内部命令结果
echo $((a+b)) #返回内部整数运算结果
```
 
*部分内容省略，请查看原博客* 
## 4. 变量
> 变量包含bash环境变量与用户自定义变量 与环境变量一致，用户自定义变量一般全大写

> 用户直接变量赋值即可，不需要对变量声明变量类型

>读取变量，在变量前加一个$ 取变量值 也可以使用${NAME}


```bash
env #查看当前环境变量
NAME = test.txt; USER = "XDU FOX" # ';'分割 变量的值含空格用“”包起来
export HOME=/fox/fox #用于向子Shell传递变量 输出变量 子Shell指在该Shell执行后执行的Shell程序
$? #上一条指令的执行结果 0为执行成功
$$ #当前Shell的PID
$0 #当前Shell的名称
$- #当前Shell的启动参数
$@ #当前脚本的参数数量
$# #当前脚本的参数值
declare #声明变量并添加对应限制
```
## 5.字符串操作
```bash
echo ${#string} #获取string的string的字符长度
echo ${string:offset:length} #返回string offset起的length长度的子字符串 string只应该变量 length可省略
echo ${string^^} #大写
echo ${string,,} #小写
```
## 6.算术运算
> ((*)) 语法支持**整数运算** 加减乘除 余数(%) 指数** 自增自减(++ --)

>进制与位运算

```bash
#数值进制
#number 默认为十进制
#0number 八进制
#0xnumber 十六进制
#base#number base进制
#位运算
>>number  #数字右移number位运算 
&   #两个数字所有位进行AND操作
|   #两个数字所有位进行OR操作
`   #数字每位取反
^   #两个数字所有位进行异或操作
#逻辑运算
expr1?expr2:expr3 三元运算符
```
## 7. 脚本入门
> SheBang行 指定解释器 以#!开始 一般为/bin/bash /bin/sh

>脚本权限控制
```bash
chmod +x script.sh 
#给所有用户运行权限
chmod +rx script.sh; chmod 755 script.sh
#给所有用户运行读取权限
chmod u+rx script.sh; chmod 700 script.sh
#只给拥有者运行读取权限
```
>env指令 适用于兼容不同环境
```bash
#!/usr/bin/env bash #在环境变量PATH中寻找bash环境
```
## 8. 条件判断
if语句判断
```bash
#if后的command 可以是一个条件判断也可以是一个命令 执行逻辑为条件判断为真或命令执行成功（返回值为0）
#if后可以带多个command 但最终结果只关注最后一个command的结果
if command; then # eg. test $USER = 'fox'; echo $USER;
      command;
elif command; then #else elif可继续进行判定
      command;
fi
```
test命令
```bash
#三者等价
test expression;
[expression];
[[expression]]; #支持正则判断
#文件判断
[ -arg file ]  # -a 是否存在 -b 是否是一个块文件 ...
#字符串判断
[ -arg string] # 无参数 判断string是否为空...
#整数判断
[integer1 -eq integer2] #等于
[integer2 -ne integer2] #不等
[integer2 -le integer2] #小于等于
[integer2 -lt integer2] #小于
[integer2 -ge integer2] #大于等于
[integer2 -gt integer2] #大于
#正则判断
[[string =~ regex]]
#逻辑运算 and or not
test1 && test2
test1 || test2
! test1
! \(test\) #使用括号时需要先转义
```
算术判断
>根据算术运算结果进行分析 返回值为0 对应false 与test相反
```bash
if ((2 > 3)) then 
if ((test = 5)) # 赋值运算 返回给if的值为5 true
```
case结构
>用于多值判断
```bash
case expression in
  pattern ) #pattern支持正则表达
    commands ;;
  pattern )
    commands ;;
  ...
esac
```
## 9. 循环
while循环结构
```bash
while condition; do #同理，condition既可以做判断条件也可以是一条指令
      commands;
done
```
until循环结构
```bash
until condition; do #与while可相互转换
      commands;
done
```
for... in 循环
```bash
for variable in list #list可由正则表达式生成 或者通配符
do
      commands
done
```
for循环
```bash
for ((expression1;expression2;expresion3)) 
do
      commands
done
```
break与continue
## 10. 函数 
函数声明方式
```bash
fun() {
      codes
}
function fun() {
      codes
}
```
>函数参数在声明阶段不进行定义，函数内部使用参数时，与脚本参数一致 使用$1 , $2 来调用参数
```bash
hello() {
  echo "Hello $1"
}
#result:
$ hello world
Hello world
```
return语句
```bash
fun hello() {
      return hello,world
      return  #空返回
}
```
**在函数内定义的变量是全局变量**

## 11. 数组
创建数组（数组赋值）
```bash
#逐个赋值 
array[0] = val0
array[1] = val1
#一次性赋值
ARRAY=(value1 value2 ... valueN)
#指定位置赋值
array=([2]=c [0]=a [1]=b)
#配合通配符
mp3s = (*.mp3) #当前目录下所有mp3文件
#只声明
declare -a ARRAYNAME
#配合read
read -a array #将用户输入赋值给数组
```
读取数组
>读取单个元素
```bash
echo ${array[0]}
echo $array[0] #会识别为$array (输出数组第一个元素)与[0] 
```
>读取所有元素
```bash
echo ${array[@]} equal echo ${array[*]}
echo "${array[@]}" #推荐使用此语法 可以避免错误 详细查看博客
not equal echo "${array[*]}" #将所有成员以单字符串返回
```
数组长度
```bash
${#array[*]}
${#array[@]}
echo ${#a[100]} #会返回a[100]的长度
```
提取数组序号（查看数组哪些位置有值）
```bash
echo ${!arr[@]}
echo ${!arr[*]}
```
数组追加
```bash
array = (a b c)
array += (d e f)
```
删除数组元素
```bash
unset array[2]
```
**关联数组（类似Map的数据结构）**
>使用declare声明
```bash
declare -A colors
colors["red"]="#ff0000"
colors["green"]="#00ff00"
colors["blue"]="#0000ff"
```
## 12. set命令
>脚本会在一个子Shell中执行，set命令可控制子Shell环境
>建议set命令写在脚本开始
```bash
set -u #自动忽略不存在变量
set -e #脚本只要发生错误就终止执行
set +e #关闭set -e选项
#管道命令，就是多个子命令通过管道运算符（|）组合成为一个大的命令
set -o pipefail #检测管道命令是否失败
set -E #在-e选项的基础上增加了trap命令捕捉
```
## 13. 脚本错误检测
编写脚本考虑项
>编写脚本时，考虑脚本命令失败的情况
```bash
#condition1
cd $dir_name
rm *
#condition2
cd $dir_name && rm *
#condition3
[[ -d $dir_name ]] && cd $dir_name && rm *
```
指令打印
```bash
#condition1
$ bash -x script.sh
#condition2
#! /bin/bash -x 
```
检测常用环境变量
>LINENO 返回当前列号    
>FUNNAME 当前函数调用栈       
>BASE_SOURCE 当前脚本调用栈
## 14.临时文件问题
>使用临时文件时，往往导致安全问题（权限授权给全用户）
>各种问题
mktemp命令
```bash
mktemp #直接生成一个临时文件，文件名随机 只有本人用户可以读写
mktemp -d #生成临时目录
mktemp -p /fox/ #指定生成随机文件所在路径 默认为 /tmp
mktemp -t temp.xxx #指定随机文件名模板
```
trap命令
>用于在bash脚本中响应系统信号       
>只能捕捉在其代码下方出现的系统信号  
>可以用函数包装多条指令
```bash
trap [动作1] [信号1] [信号2]
trap 'rm -f "$TMPFILE"' EXIT
```
