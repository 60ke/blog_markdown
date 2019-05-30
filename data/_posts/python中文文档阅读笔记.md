---
title: python中文文档阅读笔记
date: 2019-04-02 07:46:00
categories: default
tags: []
urlname: 109
---
当在序列中循环时，用 enumerate() 函数可以将索引位置和其对应的值同时取出

```python
>>>
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
...
0 tic
1 tac
2 toe
```
5.1.2. 列表作为队列使用¶
列表也可以用作队列，其中先添加的元素被最先取出 (“先进先出”)；然而列表用作这个目的相当低效。因为在列表的末尾添加和弹出元素非常快，但是在列表的开头插入或弹出元素却很慢 (因为所有的其他元素都必须移动一位)。

若要实现一个队列， collections.deque 被设计用于快速地从两端操作。例如

```python
>>>
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```
比较操作可以传递。例如 a < b == c 会校验是否 a 小于 b 并且 b 等于 c。


花括号或 set() 函数可以用来创建集合。注意：要创建一个空集合你只能用 set() 而不能用 {}，因为后者是创建一个空字典，这种数据结构我们会在下一节进行讨论。

以下是一些简单的示例：

```python
>>>
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # fast membership testing
True
>>> 'crabgrass' in basket
False

>>> # Demonstrate set operations on unique letters from two words
...
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
类似于 列表推导式，集合也支持推导式形式

>>>
>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'r', 'd'}
```
布尔运算符 and 和 or 也被成为 短路 运算符：它们的参数从左至右解析，一旦可以确定结果解析就会停止。例如，如果 A 和 C 为真而 B 为假，那么 A and B and C 不会解析 C。当作用于普通值而非布尔值时，短路操作符的返回值通常是最后一个变量。
```python
>>> string1, string2, string3 = '', 'Trondheim', 'Hammer Dance'
>>> string1 or string2
'Trondheim'
>>> string3 or string2
'Hammer Dance'
>>> string2 or string3
'Trondheim'
>>> string1 or string2 or string3
'Trondheim'
>>> 
```
格式化字符串字面值 （常简称为 f-字符串）能让你在字符串前加上 f 和 F 并将表达式写成 {expression} 来在字符串中包含 Python 表达式的值。

可选的格式说明符可以跟在表达式后面。这样可以更好地控制值的格式化方式。以下示例将pi舍入到小数点后三位:

```python
>>>
>>> import math
>>> print(f'The value of pi is approximately {math.pi:.3f}.')
The value of pi is approximately 3.142.
```
在 ':' 后传递一个整数可以让该字段成为最小字符宽度。这在使列对齐时很有用。:

```python
>>>
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
>>> for name, phone in table.items():
...     print(f'{name:10} ==> {phone:10d}')
...
Sjoerd     ==>       4127
Jack       ==>       4098
Dcab       ==>       7678
```
其他的修饰符可用于在格式化之前转化值。 '!a' 应用 ascii() ，'!s' 应用 str()，还有 '!r' 应用 repr():

```python
>>>
>>> animals = 'eels'
>>> print(f'My hovercraft is full of {animals}.')
My hovercraft is full of eels.
>>> print(f'My hovercraft is full of {animals!r}.')
My hovercraft is full of 'eels'.
```