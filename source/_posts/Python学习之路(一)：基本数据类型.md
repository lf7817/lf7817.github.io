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
type(5 // 3)    # class 'int' 向下取整等于1
```
<!--more-->

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