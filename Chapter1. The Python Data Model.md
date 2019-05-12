# Chapter1. The Python Data Model

[TOC]

## special / magic / dunder methods

Python 最大的特性，在于其语言的一致性。其定义了大量的与自然语言相近的魔法方法，用来保证语言的统一和一致性。当我们接触一个新的 Python 包时，我们能根据这些魔法方法，快速上手这个 Python 包。

魔法方法分为两类：

* magic method 

  | magic method | built-in method |
  | ------------ | --------------- |
  | `__str__`    | `str()`         |
  | `__len__`    | `len()`         |
  | `__int__`    | `int()`         |

* magic method for operators

  | magic method for operators | built-in operator |
  | -------------------------- | ----------------- |
  | `__and__`                  | `and`             |
  | `__or__`                   | `or`              |
  | `__add__`                  | `+`               |

**魔法方法的优点**：

* 魔法方法统一了常见的语法规则

  用户不需要再去记忆，对于获取一个对象的长度，究竟是用 .length() 还是 .size()

* 实现了魔法方法的类可以方便的调用 Python 的标准库（不需要自己重复造轮子）

  例如，通过实现 `__len__` 和 `__getitem__` 这两个魔法方法，该类就拥有了 list 特性，几乎所有 list 的方法都能适用

* 魔法方法的执行速度很快（其由 Python 解释器直接执行）

  Python 解释器会将 built-in 方法解释成其对应的 `__method__`魔法实现，然后执行这些魔法方法，Python解释器是这些魔法方法最频繁的执行者。

通过实现这些魔法方法，使得我们自定义的类，能够像 Python 的 built-in 类型一样用起来很方便。当我们想要创建一个新的类时，我们不仅要考虑其继承自哪些类，更要考虑，要实现哪些魔法方法。

通常情况下，我们应该去实现魔法方法，而不是去直接调用这些方法，尽管我们可以直接调用。只有一个魔法方法比较特殊：`__init__`用来调用父类的 init 方法

## Tips

### `in` 与 `_contains__()` 的关系

如果不实现 `__contains__` 方法，那么 in 的操作，就会在 list 中做一个顺序遍历

### `__repr__` 和 `__str__` 的区别

* `__repr__` 是对 object 的字符串描述，`__str__` 是 `str()`的魔法方法，并且 `print(object)`会默认被解释成 `print(__repr__(object))`
* 如果没有实现 `__str__`，那么 Python 解释器会默认调用 `__repr__` 方法，所以 `__repr__` 方法更通用
* `__repr__` 在 debugging 和 logging 时会调用，`__str__` 通常用于终端用户的字符描述
* `__str__` 更多的与 `str()` 有关，而 `__repr__` 更多的与 `print()` 有关

### `__bool__` 方法与 `__len__` 的关系

`bool(object)` 会被解释成 `object.__bool__()`，如果 `__bool__()` 方法没有被定义，那么 Python 解释器会尝试调用 `object.__len__()`方法，如果返回结果为0，则为 false.

