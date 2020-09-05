#  菜鸟教程

```html
菜鸟教程[https://www.runoob.com/python3/python3-tutorial.html]
```



# 运算符

+

-

## *

1.简单的运算

2.字符串的多个连接

```python
a = '1'
a = a * 3
print (a)

```

结果： 111

3.幂运算**

```python
a = 2 ** 3
print (a)
```

结果： 8



## /

1.向下取整 ： /

2.带精度 : //

```python
a = 2 / 3 # 结果是1.5
a = 2 // 3 #结果是1
```



## 比较运算

可以直接比较

```python
23 <= a <= 24
```

## 逻辑运算:

and or not

## 位运算

同C语言一模一样

# 输入输出

输入

```python
input() #默认类型是 str
a = input(“请输入：”) # 自带提示信息
```

输出

```python
print() ## 默认自带换行符
print (a, b, c) ## 多个输出，空格分割
print (a, b, end = "") # 不换行
print (a, b, end = " ") #不换行
print (r"\n") # r / R 取消转义符 结果： \n
```

# 流程和控制语句

## 选择语句 :

```python
if statement: # 根据缩进判断是否是一个代码块
if else 
if elif else
```

## 循环语句

while:

```python
while condition: ## 没有 i++ 和 ++i
```



for:

```python
for i in range (start, end, step): # range()是内置生成序列函数[start,end) 左闭右开 (i不是下标) 3 个不一定全有
for i in str:
```

## pass 语句

Python pass是空语句，是为了保持程序结构的完整性。

