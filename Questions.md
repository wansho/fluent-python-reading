# Questions

Questions 的目的：用来回顾 Python 的重点。

## Chapter1. The Python Data Model

* Python 语言最大的特性
* 魔法方法的优点
* 魔法方法 `in` 和 `__contains__()` 的关系
* 魔法方法 `bool()` 和 `__bool__()`,  `__len__()` 的关系
* `__repr__()` 和 `__str__()` 的区别
* 解释 Duck Typing（鸭子模型）

## Chapter2. An Array of Sequences

* Builted-in Sequence 的两种分类
* Slice 不包含最后一个元素的原因
* 通过 Slice 进行逆序 sequence 的方法
* Slice Object 及其作用（Slice 对象）
* Sequence 的 Slice 赋值及其妙用
* `+ *` 和 `+=, *=` 的区别
* 生成器表达式和列表推导式的区别
* 元组的两个作用
* 元组的拆包（unpacking）和常见的应用场景
* namedtuple 和 tuple 的区别，namedtuple 的使用场景
* `enumerate()` 的作用
* `lst.sort()` 和 `sorted()` 的区别
* inplace 方法的优点和缺点
* `bisect` 模块的使用场景
* `array.array` 的特性及其优点
* `deque` 的特性及其使用场景

## Chapter3. Dictionaries and Sets

* 可以 hashable 的类型
* dict 的常见构造方法 / 弹出数据 / 随机弹出数据的方法
* dict 的 `update()` 方法的原理
* dict 查找时，处理 missing key 的 几种方式，哪两种方式更高效？原理是什么
* dict 的变体：OrderDict / Counter 的特性
* Set 有哪些特性