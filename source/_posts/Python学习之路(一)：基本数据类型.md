---
title: Python学习之路(一)：基本数据类型
date: 2018-01-15 16:42:46
tags: python
---

Python3 中有六个标准的数据类型：
- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Sets（集合）
- Dictionary（字典）
<!--more-->

# 一、Number
Number包括:
- 整数：int 无短、长整型区分
- 浮点数：float 无单精度双精度区分
- 布尔型：bool
- 复数：complex

## 1. float和int
```Python
type(1 + 1.0)   # class 'float'
type(1 * 1.0)   # class 'float'
type(2 / 2)     # class 'float'
type(5 // 3)    # class 'int' 向下取整
```
### 进制
```Python
0b11  # 二进制
0o42  # 八进制
0xFF  # 十六进制
```
### 进制转换
- to 二进制：bin(), 接收任意进制参数，返回'str'类型
- to 八进制：oct(), 接收任意进制参数，返回'str'类型
- to 十进制：int(), 接收任意进制参数，返回'int'类型
- to 十进制：hex(), 接收任意进制参数，返回'str'类型

## 2. bool
为什么bool会被归为Number？
> 在 Python2 中是没有布尔型的，它用数字 0 表示 False，用 1 表示 True。到 Python3 中，把 True 和 False 定义成关键字了，但它们的值还是 1 和 0，它们可以和数字相加。
```Python
True + 2    # 3
False + 2   # 2
int(True)   # 1
int(False)  # 0
bool(0)     # False
bool(1)     # True
# bool方法输入0、''、[]、{}、()、None 都会返回 False，其他返回True
```
## 3. complex
用小写的‘j’表示复数，如<code>36j</code>，基本用不到，以后再研究

# 二、String
单引号、双引号都可以表示字符串
```Python
'hello world'
"hello world"
```
当字符串过长，想定义多行字符串怎么办？
- 多行字符串可以三个单引号或者三个双引号
- 使用'\'来换行
```Python
'hello\
world'

'''
  hello
  world
'''     # '\n  hello\n  world\n'
# 但是下面并不会转义'\n', 使用print可以转译
'''\n  hello\n  world\n''' # '\n  hello\n  world\n'
'\n  hello\n  world\n'     # '\n  hello\n  world\n'
```

## 转义字符
转义字符用来表示：
- 特殊字符
- 无法“看见”的字符
- 与语言本身语法有冲突的字符

如果字符串里面有很多字符都需要转义，就需要加很多\，为了简化，Python还允许用r''表示''内部的字符串默认不转义(r大小写都可以)
```Python
print(r'\n')    # \n
```

## 字符串操作基本方法
### 字符串拼接

方法1：使用加号拼接
```Python
'hello ' + 'world'    # 'hello world'
```
这种方法最简单直接，但是操作效率低，因为python中字符串是不可变类型，使用加号拼接会生成新的字符串，意味着需要重新开辟内存,当连续相加时效率必然低下。（ps:看别人实验加号少的情况效率高，加号很多的情况效率低）

方法2：使用join
```Python
str = ['hello', 'world']
newStr = ''.join(str)
```
使用略复杂，但对多个字符进行连接时效率高，只会有一次内存的申请。而且如果是对list的字符进行连接的时候，这种方法必须是首选

方法3：字符串格式化，这种方法非常常用
```Python
str = '%s %s' % ('hello', 'world')
```

### 查找字符串某一位的值
```
'hello'[0]    # 'h'
'hello'[-1]   # 'o'
```
### 查找字符串某一区间的值
```
'hello world'[0:5]      # 'hello'
'hello world'[0:-1]     # 'hello worl'
'hello world'[0:]       # 'hello world'
'hello world'[0:20]     # 'hello world'
```

# List
