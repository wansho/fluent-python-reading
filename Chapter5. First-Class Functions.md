# Chapter5. First-Class Functions

从第五章开始，一直到第七章，都是在研究函数。

[TOC]

## What is First-Class Functions

Functions are treated like any other variable. Treating functions as objects. 

函数也被作为一个对象，其和对象一样，是 Python语言中的第一公民。

Demo:

```python
def factorial(n):
    """return n!"""
    return 1 if n < 2 else n * factorial(n-1)

fact = factorial # function 作为变量传递给另外一个变量
# fact 作为变量传入 map 方法，其参数为 range 生成的数据，map 返回一个 iterated 的对象
list(map(fact, range(10))) 
# 等价于
list(map(factorial, range(10)))

```

## 函数的 attributes

Demo:

```python
print(factorial.__doc__) # return n!
# __doc__ 用于生成 help text of and object
print(help(factorial))
"""
Help on function factorial in module __main__:
factorial(n)
    return n!
None
"""
```

| attribute | 解释           |
| --------- | -------------- |
| `__doc__` | 函数的注释声明 |
|           |                |
|           |                |



## 函数的 functions



## Higer-Order Functions

A function that takes a function as argument or returns a function as the result is a higher-order function.

传入或者返回一个函数的函数叫做 higer-order-function。

Higer-Order Functions: **sort, map, filter, reduce**

### Demo: sort()

```python
de reverse(word):
    """逆置word"""
    return word[::-1]
fruits = ["straberry", "fig", "cherry", "apple", "banana"]
sorted(fruits, key=reverse) # reverse 作为一个 function
# 结果为：["banana","apple", "fig", "straberry", "cherry"]
# 上述代码执行的步骤：
# 1. 根据传入的 key 函数，对 fruits 进行变换，得到变换后的 list
# 2. 对 fruits 按照变换后的规则进行排序

# 其他变换规则
sorted(fruits, key=len)
```

### Tips

* 在 Python3 中， **map** 和 **filter** 会返回一个 generator (iterable)对象，并不是一个 sequence



### Modern Replacements for map/filter/reduce

Chapter2 中已经指出，任何用到 map 和 filter 的地方，都可以用 列表推导式 和 生成器表达式来替换。Demo:

```python
list(map(factoria, filter(lambda n: n % 2, range(6)))) # list of factorial of odd numbers up to 5!, using both map and filter
```



