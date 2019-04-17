# Python-Code-Optimization

## 为什么要看 Fluent-Python

深入的学习 Python，才能了解这门语言的精髓，才能优雅的使用 Python。

Python 是一门高效的语言，但其也是一把双刃剑，使用不当的话，会耗费大量的内存和计算资源。

通过学习书中提高的指针和各种优化措施，我们能避免在编程中创建不必要的副本，帮助我们节约程序运行所占的内存。

例如，当我们想要扩展一个字符串时，我们应该

```python
ss = "Hello"
print(id(ss)) # 1746944705792
ss += "world" 
print(id(ss)) # 1746944705792
```

这样可以在 ss 原来所占内存的基础上进行内存的扩充，如果是图方便：

```python
ss = "Hello"
print(id(ss)) # 1746944705792
ss = ss + "world" 
print(id(ss)) # 1746961939120
```

那么就会重新开辟一块空间。这是一个小得不能再小的细节，很多人并不会很在意，毕竟一个小小的字符串并不会占用很大的内存空间。但是，如果我们在工作中，遇到了很长的 ss 呢（假设1KB）？而且需要频繁对 ss 进行扩展呢(一万次)？如果按照我们平时的第二种写法，那么我们每一次扩展，都是对原字符串的一次深拷贝，那么第一次拷贝内存成本都会上升，即使每次添加的字符并不多，那么拷贝一万次后，内存里至少会产生 10MB 的垃圾。如果这个脚本每隔 10 分钟就要跑一次，那么每隔 10 分钟就会产生 10MB 的垃圾（这里不考虑垃圾回收机制）。长此以往，计算机的内存就会被吃空。

## 内存优化

### 字符串 和 sequence 优化

字符串 和 sequence 的扩展，可以通过 `+` 或 `*` 实现，但是怎么用还是有讲究的。

**优化后**

```python
# 标准的字符串和 sequence 的扩展
ss = "hello"
ss += "world"
ss *= 5

list1 = [1, 2, 3]
list2 = [4, 5, 6]
list1.extend(list2)
# extend 等价于 +=
list1 += list2
list1 *= 5
```

**优化前**

```python
ss = "hello"
ss = ss + "world"
ss = ss * 5

list1 = [1, 2, 3]
list2 = [4, 5, 6]
list1 = list1 + list2
list1 = list1 * 2
```

注意：`+=`， `*=` 的优化，其只对于 mutable(可更改) 的 sequence 生效，对于 tuple 这样的 immutable sequence，`+=` 和 `+` 的效果是一样的。但是 `str` 是一个例外，由于 str 使用频率太高，所以 Python 专门针对 str 进行了优化。Fluent-Python的原文是：

> str instance are allocated in memory with room to spare, so that concatenation does not require copying the whole string every time.

**优化原理**

`+=`， `*=` 两个运算符在 Python 中被定义为 magic operator，其会被 Python 解释器解释成 `__iadd__()` 和 `__imul__()` （其中 i 是 in-place 的意思，也就是 `就地` 的意思）两个魔法方法，而普通的 `+` 和 `*` 两个运算符，则是被 Python 解释器解释成了 `__add__()` 和 `__mul__()`，所以本质上，两个被解释成了不同的魔法方法，然后执行。

## 计算优化

### 频繁进行 containment check 的优化

如果我们需要频繁的检查某个元素是否在一个 list 中，我们可以用 set 来取代 list

**优化后**

```python
if to_check_str in set(["a", "b", "c"]):
```

**优化前**

```python
if to_check_str in ["a", "b", "c"]:
```

注意：set 并不是 sequence

## 语法优化

## 换行

在括号 `[]{}()`类的换行，都不需要加入换行符 `\`，所以我们可以通过在括号内换行，写出更有层次感和可读性的列表推导式。



## API Convention

### In-place method

Functions or methods that change an object in place should return None to make it clear to the caller that the object itself was changed and no new object was created.

For example:

```python
list1 = [2,3,5,7,7,8]
list1.sort()
list1.shuffle()
```

但是，inplace 方法有一个缺点，就是无法实现 cascade operation.