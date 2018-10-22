---
title: "[Python][Class] __str__ v.s. __repr__"
date: 2018-10-22T09:54:35+08:00
draft: false
tags:
    ["PythonClass"]
categories:
    - Python
authors: ["bradlee"]
toc: false
---
**object._ _ str _ _(self) Purpose[Readability]**: return a string which is a more convenient or concise representation can be used.

**object._ _ repr _ _(self) Purpose[Unambiguous]**: return a string which should look like a valid **Python expression** that could be used to recreate an object with the same value (given an appropriate environemnt).

- If **_ _ repr _ _** is defined, and **_ _ str _ _** is not, the object will behave as though **_ _ str _ _= _ _ repr _ _**.

- Almost every object you implement **should** have a functional **_ _ repr _ _** that's usable for understanding the object.

- Implementing **_ _ str _ _** is **optional**: do that if you need a "pretty print" functionality. (for example, used by a report generator)

# Why need to implement __str__ and __repr__?
## object._ _ str _ _ (self)
Called by **str(object)** and the built-in functions **format()** and **print()** to compute the **“informal”** or nicely printable string representation of an object. The return value must be a string object.

This method differs from **object._ _ repr _ _()** in that there is no expectation that _ _ str _ _ () return a valid Python expression: **a more convenient or concise representation can be used**.

The default implementation defined by the built-in type object calls object._ _ repr _ _ ().

```python
class Car:
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __str__(self):
        return 'The color of car is {} and mileage is {}.'.format(self.color, self.mileage)

my_Car = Car('red', 1234)
print(my_Car)
'{}'.format(my_Car)
str(my_Car)
```
###  The goal of _ _ str _ _ is to be readable
The goal is to represent it in a way that a **user**, not a programmer, would want to read it.

## object._ _ repr _ _ (self)
Called by the **repr()** built-in function to compute the “official” string representation of an object. If at all possible, this **should look like a valid Python expression** that could **be used to recreate an object** with the same value (given an appropriate environment). If this is not possible, a string of the form **<...some useful description...>** should be returned. The return value must be a string object.

If a class defines _ _ repr _ _ () but not _ _ str _ _ (), then _ _ repr _ _ () is also used when an “informal” string representation of instances of that class is required.

This is typically used for **debugging**, so it is important that the representation is information-rich and unambiguous.

```python
class Car:
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __repr__(self):
        return 'Car(color=%r, mileage=%r)'%(self.color, self.mileage)

my_Car = Car('red', 1234)
print(my_Car)
'{}'.format(my_Car)
str(my_Car)
my_Car
```
Better:
```python
class Car:
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __repr__(self):
        return f'Car(color={self.color!r}, mileage={self.mileage!r})'
```
Good _ _ repr _ _ template:
```python
class Car:
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __repr__(self):
        return f'{self.__class__.__name__}(color={self.color!r}, mileage={self.mileage!r})'
```
# Reference
https://www.oschina.net/translate/difference-between-str-and-repr-in-python?cmp

https://baijiahao.baidu.com/s?id=1596817611604972751&wfr=spider&for=pc

https://docs.python.org/3.7/reference/datamodel.html?highlight=__repr__#object.__repr__
