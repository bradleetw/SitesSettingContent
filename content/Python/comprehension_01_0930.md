---
title: "[Python] Comprehensions Concepts"
date: 2018-09-30T10:42:24+08:00
draft: false
tags:
    ["PythonComprehension"]
categories:
    - Python
authors: ["bradlee"]
toc: true
---
# What is the Comprehension?
這個 Python 必須懂的高階使用概念, 在官方的資料中並沒有單獨 **comprehension** 的章節, 而是可以看到如下的詞:

- List Comprehension
- Set Comprehension
- Dict Comprehension
- Asynchronous Comprehension (New syntax features in 3.6)

而線上的資料大都從 **List Comprehension** 開始介紹這個概念. [Python List Comprehensions: Explained Visually](http://treyhunner.com/2015/12/python-list-comprehensions-now-in-color/), 這篇由 Tery Hunner 邊寫的內容, 是我看到很多人引用來介紹的文章.

**Sometimes a programming design pattern becomes common enough to warrant its own special syntax. Python’s list comprehensions are a prime example of such a syntactic sugar.** -- Tery Hunner.

而掌握這樣的概念可以帶來什麼好處?

[必会的List Comprehension （列表推导式）](https://www.jianshu.com/p/c52968ab9c3d), 來自簡書的這篇文章提到了兩點:

- 應該寫更短和更高效的代碼
- 代碼應該執行更快

所以本文章來記錄如何寫出 Comprehension , 以及紀錄實驗結果.

# What is the list comprehension?
**List comprehensions are a tool for transforming one list (any iterable actually) into another list.** - Tery Hunner.

依據 Tery 的描述, "來源物件"是否支持 **iterable** 屬性是能否使用 list comprehensions 這個工具的重點. e.g. **list**, **str**, **tuple**, **dict** 這些都可以利用這工具.

```python
target_object = []
for ITEM in source_object:
    if condition_based_on(ITEM):
        target_object.append("something with" + ITEM)
```

list comprehension: when the type of target is **list** so we call **list comprehension**.
```python
target_list = ["something with" + ITEM for ITEM in source_object if condition_based_on(ITEM)]
```

## set comprehension
When the type of target is **set** we call **set comprehension**.

```python
target_set = {"something with" + ITEM for ITEM in source_object if condition_based_on(ITEM)}
```

## dictionary comprehension
When the type of target is **dictionary** we call **dictionary comprehension**.

```python
target_dict = { key: value for key, value in source_object.items() }
```

## Generator
There is a special case in comprehension progress, the result is the **generator** type.

```python
target_gen = ("something with" + ITEM for ITEM in source_object if condition_based_on(ITEM))
```

## 可讀性
```python
target_list = [
    "something with" + ITEM
    for ITEM in source_object
    if condition_based_on(ITEM)
]
```

```python
target_dict = {
    key: value
    for key, value in source_object.items()
    if condition_based_on(value)
}
```

## Unconditional Comprehension
#### for loop type:
```python
doubled_numbers = []
for n in nubmers:
    doubled_numbers.append(n*2)
```

#### comprehension type
```python
doubled_numbers = [n*2 for n in numbers]
```
#### readable
```python
doubled_numbers = [
    n*2
    for n in numbers
]
```

## Nested Loops
#### for loop type
```python
flattened = []
for row in matrix:
    for n in row:
        flattened.append(n)
```

#### comprehension type
```python
flattened = [n for row in matrix for n in row]
```
#### readable
```python
flattened = [
    n
    for row in matrix
    for n in row
]
```

# Reference
[The Pythonn Tutorial - Regarding to List Comprehensions](https://docs.python.org/3/tutorial/datastructures.html#tut-listcomps)

[Python List Comprehensions: Explained Visually](http://treyhunner.com/2015/12/python-list-comprehensions-now-in-color/)

[必会的List Comprehension （列表推导式）](https://www.jianshu.com/p/c52968ab9c3d)
