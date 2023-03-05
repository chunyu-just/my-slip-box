### 函数

为函数取名（为变量取名也一样）有些基本的注意事项：

> - 首先，名称不能以数字开头。能用在名称开头的有，大小写字母和下划线 `_`；
> - 其次，名称中不能有空格，要么使用下划线连接词汇，如，`do_nothing`，更推荐使用下划线；
> - 再次，名称不能与关键字重合 —— 以下是 Python 的 Keyword List：

|     -      | Python     | Keyword    | List       |     -      |
| ---------- | ---------- | ---------- | ---------- | ---------- |
| `and`      | `as`       | `assert`   | `async`    | `await`    |
| `break`    | `class`    | `continue` | `def`      | `del`      |
| `elif`     | `else`     | `except`   | `False`    | `finally`  |
| `for`      | `from`     | `global`   | `if`       | `import`   |
| `in`       | `is`       | `lambda`   | `None`     | `nonlocal` |
| `not`      | `or`       | `pass`     | `raise`    | `return`   |
| `True`     | `try`      | `while`    | `with`     | `yield`    |

你随时可以用以下代码查询关键字列表：

```python
import keyword
keyword.kwlist 列出所有的关键字
keyword.iskeyword('if')      # 查询某个词是不是关键字
```

- 把函数当作产品，你是产品的用户
- 读产品说明书，关注函数再使用时需要注意什么
- 所有函数都有返回值，即使其内部不指定返回值，也有一个默认的返回值: None
- 

```py
func(*arg, *kwarg)
```

- arg 位置参数，由位置决定其值的参数
    - 必须要有的参数，必须要按顺序，如：divmod(a,b)
    - 可选择的参数,如：pow(x,y[,z]) z为可选择的参数，其参数输入可以为(x,y)或(x,y,z)
    - 可接受很多值的位置参数
        - 函数只有一个位置参数：print(*object)
        - 有多个位置参数，接受很多值的arg要放到后面：max(arg1,arg2,*arg[,key])
- kwarg 关键字参数，其定义带有`=`
    - **kwarg 可以接受很多值的关键字参数
        - 在函数内部，处理其使用的是对字典的迭代方式，在调用时，也可以直接使用字典的形式，函数内部也可以用迭代的方式处理这个字典，见下方代码

- 函数参数的顺序
    - 1. Positional
    - 2. Arbitrary Positional
    - 3. Keyword
    - 4. Arbitrary Keyword


```python
def say_hi(**names_greetings):
    for name, greeting in names_greetings.items(): # item()方法返回字典的 key 和 value
        print(f'{greeting}, {name}!')
        
a_dictionary = {'mike':'Hello', 'ann':'Oh, my darling', 'john':'Hi'}

say_hi(**a_dictionary)
print("----------------------")
say_hi(**{'mike':'Hello', 'ann':'Oh, my darling', 'john':'Hi'})
```

    Hello, mike!
    Oh, my darling, ann!
    Hi, john!
    ----------------------
    Hello, mike!
    Oh, my darling, ann!
    Hi, john!


匿名函数 lambda
```python
name = lambda x, y: x + y
```
- <关键字> <参数>: <表达式> 表达式的值就是这个函数的返回值

- 应用场景
    - 作为另一个函数的返回值
    
    - 作为某函数的参数 比如
    
        ```python
        map(function,iterable,...)
        
        c_list = list(map(lambda x: x * 2, a_list))
        ```
    

### 文档 Docstring

在函数定义内部，我们可以加上 **Docstring**；将来函数的 “用户” 就可以通过 `help()` 这个内建函数，或者 `.__doc__` 这个 Method 去查看这个 Docstring，即，该函数的 “产品说明书”。
- 用""" doc """ 可多行，可单行
- 必须在函数定义的内部语句块的开头
- 必须同其他部分一样保持缩进
- 它有自己的规范

### 模块


```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```

- 每一个`.py`文件都可以是个模块，可以被引用
- `dir(module)` 函数查看模块内部可触达的变量名称和函数名称

### 可执行的python文件

把程序封装到`main()`中，如：
```python
    ...
    def main():
    routine_1()
    routine_2()
    print('This is the end of the program.')
    
if __name__ == '__main__':
    main()
```

当一个模块（`.py` 文件，例如：`mycode.py`）被 `import` 语句导入的时候，这个模块的 `__name__` 就是模块名（例如：`'mycode'`）。

而当一个模块被命令行运行的时候，这个模块的 `__name__` 就被 Python 解释器设定为 `'__main__'`。

把一个程序整个封装到 `main()` 之中，而后在模块代码里加上：

```python
if __name__ == '__main__':
    main()
```

这么做的结果是：

> 1. 当 Python 文件被当作模块，被 `import` 语句导入时，`if` 判断失败，`main()` 函数不被执行；
> 2. 当 Python 文件被 `python -m` 运行的时候，`if` 判断成功，`main()` 函数才被执行。
> **像 `that.py` 那样把整个程序放进 `main()` 函数之后，`import that` 不会自动执行 main 函数里的代码。不过，你可以调用 that.main()：**

### 字符串


```python
# 字符码表 unicode
ord("a") # 字符转码 -> 97
chr(122) # 码转字符 -> 'z'
```


```python
# 字符串 与 数值
int('3') # 数字型字符 转 整数 -> 3
float('4') # 浮点型           -> 4.0
str(3.12)  #                  -> 3.12
```

`intput()`接受用户输入，将其作为*字符串*返回


```python
"""
多行字符串注释
"""
```

### 字符串操作符

- 字符串可用`' '`或者` + `拼接

- 字符串与数字用` * `连接，`'Ha' * 3` 的意思是说，把字符串 `'Ha'` 复制三遍

- in 或 out 操作符，查看某个字符/串是否包含在某个字符串中，返回布尔值，如：

  ```python
  'o' in 'Hey, You!' # -> True
  ```

### 字符串索引

- 字符串为*有序容器*
- 从 0 开始索引
- 我们可以使用*索引操作符*根据*索引**提取**字符串这个*有序容器*中的*一个或多个元素，即，其中的字符或字符串。这个 “提取” 的动作有个专门的术语，叫做 “Slicing”（切片）。索引操作符 `[]` 中可以有一个、两个或者三个整数参数，如果有两个参数，需要用 `:` 隔开。它最终可以写成以下 4 种形式：
> * `s[index]` —— 返回索引值为 `index` 的那个字符
> * `s[start:]` —— 返回从索引值为 `start` 开始一直到字符串末尾的所有字符
> * `s[start:stop]` —— 返回从索引值为 `start` 开始一直到索引值为 `stop` 的那个字符*之前*的所有字符
> * `s[:stop]` —— 返回从字符串开头一直到索引值为 `stop` 的那个字符*之前*的所有字符
> * `s[start:stop:step]` —— 返回从索引值为 `start` 开始一直到索引值为 `stop` 的那个字符*之前*的，以 `step` 为步长提取的所有字符
- 提醒：无论是 `range(1,2)`，或者 `random.randrange(100, 1000)` 又或者 `s[start:stop]` 都有一个相似的规律，包含左侧的 `1`, `100`, `start`，不包含右侧的 `2`, `1000`, `stop`。

### 字符串的 method

- 字符串是 str 类的对象
- 每个类（Class）内都有方法 method
- str 的方法
    - `str.upper()` 字符串大写
    -   `lower()` 字符串小写
    -   `swapcase()` 逐个字符更换大小写，大变小，小变大
    -   `casefold()` 转成小写，可以转换欧洲字符
    -   `capitalize()` 行首字母大写
    -   `title() `每个词首字母大写
    - `str.encode()` 处理非英文字符串如中文
- 搜索
    - `str.count(sub[, strat[,end=len(str)]])` sub要搜的字符
    - `startswith()` 判断是否以某个字符串开始，返回布尔值
    - `endswith()`                     … 结束
    - `find(sub[, strat[,end=len(str)]])` 找到最早的位置，没找到返回 -1
    - `rfind(sub[, strat[,end=len(str)]])` 找到最后出现的位置，没找到返回 -1
    - `index(sub[, strat[,end]])` 与find类似，没找到触发错误
    - `rindex()`与`rfind()`类似
- 替换
    - `str.replace(old, new[, count])` 用 `new` 替换 `old`，替换 `count` 个实例（实例：example，每次处理的对象就是实例，即具体的操作对象），其中，`count` 这个参数是可选的。
    - `str.expandtabs(tabsize= 8)` 默认用 8 (数字可以替换)个空格替换 tab(\t)
- 去除子字符
    - `str.strip([chars])` 去除一个字符串首尾的所有空白，包括空格、TAB、换行符，给定了一个字符串作为参数，那么参数字符串中的所有字母都会被当做需要从首尾剔除的对象，直到新的首尾字母不包含在参数中，就会停止剔除
    - `lstrip()` 只对左侧处理
    - `rstrip()` 只对右侧处理
- 拆分字符串
    - `splitline()` 返回个列表，去除\n，然后拆分
    - `split(sep=None, maxsplit=-1)` 那么默认为用 None 分割(各种空白，比如，\t 和 \r 都被当作 None)，其内容可以更改
- 拼接子字符串
    - `join(_iterable_)`
- 字符串排版
    - `str.center(width[, fillchar])` 第二个参数只接受单个字符
    - `ljust(width)` 靠左对齐
    - `rjust(width)` 靠右对齐
    - `str(i).zfill(3)` 将字符串转换成左侧由 `0` 填充的指定长度字符串。例如，这在批量生成文件名的时候就很有用
- 格式化字符串
    - `format(*args, **kwargs)` 索引位置灵活 0 ，1位置可以呼唤
        
        ```python 
            '{0} is {1} years old.'.format(name, age)
        ```
    - f-string 更方便
        ```python
            name = 'John'
            age = 25
            f'{name} is {age} years old.' 
        ```


### 元组

- 元组不可变有序数列，不可删元素
- 列表可变有序数列
- 在将来需要更改的时候，创建 List
- 在将来不需要更改的时候，创建 Tuple
- 其次，从计算机的角度来看，Tuple 相对于 List 占用内存小
- 元组的创建 a = (2,) 不要忘记 ','
- 

### 集合

- 用`{ }`括起来，用`','`隔离开
- 创建空集合 必须用 set()
- set 不包含重合元素，无序，
    - 集合分可变 set，不可变 frozen
- 将带重复数据的序列转换成集合后，返回一个去重的集合
- set相关操作
    - `in`
    - `len( )`
    - `max( )`
    - `min( )`
    - 可变集合 `set.remove(elem)` , frozen 集合不用
    - 操作符 '|'并 '&'交 '-'差 '^'对称差集
    - set 也有对应操作符的方法可以调用，用到时候再查
    - set 也可以进行逻辑运算
- set自身的方法
    - `add( )`
    - `remove( )`
    - `discard( )` 若元素存在于集合中，删除它
    - `pop` 随机删除
    - `clear` 删除全部

`**set.update**(*_others_)`，相当于 `set |= other | ...`

> 更新 set, 加入 others 中的所有元素；

**`set.intersection_update**(*_others_)`，相当于 `set &= other & ...`

> 更新 set, 保留同时存在于 set 和所有 others 之中的元素；

**`set.difference_update**(*_others_)`，相当于 `set -= other | ...`

> 更新 set, 删除所有在 others 中存在的元素；

**`set.symmetric_difference_update**(_other_)`，相当于 `set ^= other`

> 更新 set, 只保留存在于 set 或 other 中的元素，但不保留同时存在于 set 和 other 中的元素；**注意**，该 Method *只接收一个参数*。

### 字典

- ```python 
     sss = {'a':1, 'b':2, 'c':3}
  ```
- key 唯一
- 更新某元素 直接对其元素进行赋值
- 添加元素
    - `dic.update(dic2)`
- 删除元素
    - `del sss['a']`
- 逻辑运算符 `in`
- 内建函数
    - `update`
    - `len`
    - `max`
    - `min`
    - `list`
    - `set`
    - `tuple()`
    - `sorted()`
    - `sorted(dic, reverse=True)`
- 方法
    - `dic.copy()` copy的原件不发生改变
    - `clear` 清空
    - `popitem`
    - `pop(key,value)`
    - `get(key,value)`
    - `setdefalut(key,item)`

### 迭代

- 用 `for 循环`进行迭代 `range（）`和 list
- 迭代的同时获得索引
```py
        for i, t in enumerate(t):
            print(i, t)
```
- 迭代前可排序
```python 
    for i, t in enumerate(sorted(t))
```
- 同时迭代多个容器
    - `zip()` 同时迭代两个或两个以上容器中的元素
    ```py
        chars = 'abcdefghijklmnopqrstuvwxyz'
        nums = range(1, 27)
        for c, n in zip(chars, nums):
            print(f"Let's assume {c} represents {n}.")
    ```
- 迭代字典中的元素
```py
        for key in phonebook1:
    print(key, phonebook1[key])
        for key, value in phonebook1.items():
    print(key, value)
```


### 文件

- 要有 os 包
> `open(file, mode='r')`

第二个参数，`mode`，默认值是 `'r'`，可用的 `mode` 有以下几种：

| 参数字符 | 意义                            |
| -------- | ------------------------------- |
| `'r'`    | 只读模式                        |
| `'w'`    | 写入模式（重建）|
| `'x'`    | 排他模式 —— 如果文件已存在则打开失败 |
| `'a'`    | 追加模式 —— 在已有文件末尾追加      |
| `'b'`    | 二进制文件模式                  |
| `'t'`    | 文本文件模式（默认）|
| `'+'`    | 读写模式（更新）|

- 一般这么用

  ```python
  f = open('/githubcode/xiaolai/the-craft-of-selfteaching/test-file.txt', 'w')
  print(f.name)
  f.close()
  ```

读写文件
- `f.close()`
- `f.read`
- `f.write`
- `f.reafline()` 每调用一次，返回新一行
- `f.readlines()` 将文件作为一个列表返回，列表中的每个元素对应着文件中的每一行
- `file.writelines()` 把一个列表写入到一个文件中，按索引顺序（从 0 开始）逐行写入列表的对应元素

`with 语句` 不用写 `close()`

 ```python
 with open(...) as f:
    f.write(...)
 ```

### 函数工具

#### 迭代器 iterator

- python 的所有容器，都是可通过迭代遍历每一个元素
- `iter()` 把可迭代对象转换成迭代器
    - `i = iter("python")` 字符串，元组，列表 都行
    - 通过 `next(i)` 返回遍历到的元素


```python
"""
迭代器是个 Object
写迭代器的时候写的是 Class
比如我们写一个数数的迭代器Counter 
"""
class Counter(object):
    def __init__(self, start, stop):
        self.current = start
        self.stop = stop

    def __iter__(self):
        return self
    def __next__(self):
        if self.current > self.stop:
            raise StopIteration
        else:
            c = self.current
            self.current += 1
        return c

c = Counter(11, 20)
next(c)
next(c)
next(c)

for c in Counter(101, 105):
    print(c, sep='')
type(Counter)

c = Counter(201, 203)
while True:
    try:
        print(next(c), sep=', ')
    except StopIteration:
        break
```


    '\n迭代器是个 Object\n写迭代器的时候写的是 Class\n比如我们写一个数数的迭代器Counter \n'


    11


    12


    13

    101
    102
    103
    104
    105

    type

    201
    202
    203


这里的重点在于两个函数的存在，
`__iter__(self)` 和 `__next__(self)`。


```python
def __iter__(self):
    return self
```
默认写法，写上它们，`Counter` 这个类就会被识别为 Iterator。
而后再有 `__next__(self)` ，形成一个完整的迭代器。除了可以用 `for loop` 之外，也可以用 `while loop` 去遍历迭代器中的所有元素：

#### 生成器 generate

那用函数（而不是 Class）能不能写一个 Counter 呢？答案是能，用生成器（Generator）就行。


```python
def counter(start, stop):
    while start <= stop:
        yield start
        start += 1
for i in counter(101, 105):
    print(i)
```

    101
    102
    103
    104
    105


- `yield` 语句之后的语句仍然会被执行，`return`后的语句被忽略
- 写生成器只能用 yield 
- 生成器函数被 `next()` 调用后，执行到 `yield` 生成一个值返回（然后继续执行 `next()` 外部剩余的语句）；下次再被 `next()` 调用的时候，从上次生成返回值的 `yield` 语句处继续执行

生成器表达式
```python
even = (e for e in range(10) if not e % 2)
```
看着和列表生成式一样，但不一样
- 列表生成式 最外侧是 [ ]
- 生成器表达式最外侧是 ( )
- 集合生成式 最外侧是 { }


#### 装饰器 Decorator

- 函数也是python中的对象
- 函数本身可作为别的函数的 参数 和 返回值
- return func 返回的是这个函数本身
- return func() 返回的是对这个函数的调用
- 装饰器的操作符`@`


```python
def a_decorator(func):
    def wrapper():
        print('We can do sth. before calling a_func...')
        func()
        print('... and we can do sth. after it was called...')
    return wrapper # 返回的是函数本身

@a_decorator
def a_func():
    print("-------Hi, I'm a_func!")
    
a_func()
```

    We can do sth. before calling a_func...
    -------Hi, I'm a_func!
    ... and we can do sth. after it was called...


以上代码等价于下面代码


```python
def a_decorator(func):
    def wrapper():
        print('We can do sth. before a func is called...')
        func()
        print('... and we can do sth. after it is called...')
    return wrapper() # 返回的是函数的调用

def a_func():
    print("--------Hi, I'm a_func!")
a_func()
print('\n') 

a_decorator(a_func)
```

    --------Hi, I'm a_func!

    We can do sth. before a func is called...
    --------Hi, I'm a_func!
    ... and we can do sth. after it is called...


在我们定义 `a_func()` 的时候，在它之前，加上了一句 `@a_decorator`；这么做的结果是：

> 每次 `a_func()` 在被调用的时候，因为它之前有一句 `@a_decorator`，所以它会先被当作参数传递到 `a_decorator(func)` 这个函数中…… 而后，真正的执行，是在 `a_decorator()` 里被完成的。

—— 被 `@` 调用的函数，叫做 “装饰器”（Decorator)，比如，以上代码中的 `a_decorator(func)`。

现在可以很简单直接地说清楚装饰器的作用了：

```python
@a_decorator
def a_func():
    ...
```

等价于

```python
def a_func():
    ...
a_func = a_decorator(a_func)
```

就是用 `a_decorator` 的调用结果替换掉原来的函数。`a_decorator` 返回值是什么，以后调用 `a_func` 时就是在调用这个返回值，而 `a_decorator` 本身此时已经执行完毕了。

##### 装饰器的用途

Decorator 最常用的场景是什么呢？最常用的场景就是用来改变其它函数的行为。


```python
def an_output():
    return 'time'
print(an_output())
```

    time

```python
def uppercase(func):
    def wrapper():
        modified_restult = func().upper()
        return modified_restult
    return wrapper

@uppercase
def an_output():
    return 'time'
print(an_output())
```

    TIME


你还可以给一个函数加上一个以上的装饰器：


```python
def uppercase(func):
    def wrapper():
        original_result = func()
        modified_restult = original_result.upper()
        return modified_restult
    return wrapper
def strong(func):
    def wrapper():
        original_result = func()
        modified_restult = '<strong>'+original_result+'</strong>'
        return modified_restult
    return wrapper

@strong
@uppercase
def an_output():
    return 'The quick brown fox jumps over the lazy dog.'
print(an_output())

print("----------------------------------------------")

# 将两个装饰器调换位置
@uppercase
@strong
def an_output():
    return 'The quick brown fox jumps over the lazy dog.'
print(an_output())
```

    <strong>THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG.</strong>
    ----------------------------------------------
    <STRONG>THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG.</STRONG>

**装饰器的执行顺序是 “自下而上” —— 其实是 “由里到外” 更为准确**

##### 装饰带有参数的函数

到现在我们见到的使用装饰器的函数都是没有参数的：`an_output` 以及之前的 `a_func`。

如果被装饰的函数有参数怎么办？装饰器自身内部又应该怎么写？

这时候，Python 的 `*args` and `**kwargs` 的威力就显现出来了 —— 之前怕麻烦没有通过仔细反复阅读搞定这 “一个星号、两个星号、直接晕倒” 的知识点的人，现在恐怕要吃亏了……

装饰器函数本身这么写：

```python
def a_decorator(func):
    def wrapper(*args, **kwargs):
        return original_result
    # ...   
    return wrapper
```

在这里，`(*args, **kwargs)` 非常强大，它可以匹配所有函数传进来的所有参数…… 准确地讲，`*args` 接收并处理所有传递进来的位置参数，`**kwargs` 接收并处理所有传递进来的关键字参数。

假设我们有这么个函数：


```python
def say_hi(greeting, name=None):
    return greeting + '! ' + name + '.'

print(say_hi('Hello', 'Jack'))
```

    Hello! Jack.


如果我们想在装饰器里对函数名、参数，都做些事情 —— 比如，我们写个 `@trace` 用来告诉用户调用一个函数的时候都发生了什么……


```python
def trace(func):
    def wrapper(*args, **kwargs):
        print(f"Trace: You've called a function: {func.__name__}(),",
              f"with args: {args}; kwargs: {kwargs}")
    
        original_result = func(*args, **kwargs)
        print(f"Trace: {func.__name__}{args} returned: {original_result}")
        return original_result
    return wrapper

@trace
def say_hi(greeting, name=None):
    return greeting + '! ' + name + '.'

print(say_hi('Hello', name='Jack'))
```

    Trace: You've called a function: say_hi(), with args: ('Hello',); kwargs: {'name': 'Jack'}
    Trace: say_hi('Hello',) returned: Hello! Jack.
    Hello! Jack.


### 面向对象 oop

面向对象编程（OOP），是使用**对象**（Objects）作为核心的编程方式。进而就可以把对象（Objects）的数据和运算过程**封装**（Encapsulate）在内部，而外部仅能根据事先设计好的**界面**（Interface）与之沟通。

程序设计过程中，要对标现实世界创造对象，我们用的手法是抽象
- 抽象，把没必要的细节去掉，留主要特征
- 属性，保留下来的主要特征，叫做对象的属性【名词】
- 方法，抽象后被保留下来的必要行为，叫做对象的方法【动词】

在程序中创建对象时，做法：
- 先创建最抽象的类 Class
- 再创建子类 Subclass
- 创建实例，创建好狗这个类后，就可以根据这个狗创建很多条狗，这很多条狗就是狗的这个实例
子类 与 父类 之间是*继承*关系，哺乳动物有头，狗就有头

一些术语
> * 对象，封装，抽象
> * 界面，属性，方法
> * 继承，类，子类，实例

**你可以这样分步理解：**

> * 你创造了一个类（Class），这时候你是创作者，从你眼里望过去，那就是个类（Class）；
> * 而后你根据这个类的定义，创建了很多实例（Instances）；
> * 接下来一旦你开始使用这些实例的时候，你就成了使用者，从使用者角度望过去，手里正在操作的，就是各种对象（Objects）……

#### Defining Class

Class 使用 `class` 关键字进行定义。
Class 接收参数不是在 `class Classname():` 的括号里完成


```python
import datetime

class Golem:
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
    
    def say_hi(self):
        print('Hi!')
        
g = Golem('Clay')
g.name
g.built_year
g.say_hi
g.say_hi()
type(g)
type(g.name)
type(g.built_year)
type(g.__init__)
type(g.say_hi)
```


    'Clay'


    2023


    <bound method Golem.say_hi of <__main__.Golem object at 0x0000028AB4202280>>

    Hi!

    __main__.Golem


    str


    int


    method


    method

**下文的解释很重要**

以上，我们创建了一个 Class:

```python
class Golem:
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
```

其中定义了当我们根据这个 Class 创建一个实例的时候，那个 Object 的初始化过程，即 `__init__()` 函数 —— 又由于这个函数是在 Class 中定义的，它为 Class 的一个 Method。

这里的 `self` 就是个变量，系统默认可以识别的变量，指代将来用这个 Class 创建的 Instance。

如，创建了 Golem 这个 Class 的一个 Instance，`g = Golem('Clay')` 之后，我们写 `g.name`，那么解析器就去找 `g` 这个实例所在的 Scope 里有没有 `self.name`……

注意：`self` 这个变量的定义，是在 `def __init__(self, ...)` 这一句里完成的。对于这个变量的名称取名没有强制要求，你实际上可以随便用什么名字，很多 C 程序员会习惯于将这个变量命名为 `this` —— 但根据惯例，你最好还是只用 `self` 这个变量名，省得给别人造成误会。

在 Class 的代码中，如果定义了 `__init__()` 函数，那么系统就会将它当作“ Instance 在被创建后初始化的函数”。这个函数名称是强制指定的，初始化函数必须使用这个名称；注意 `init` 两端各有两个下划线 `_`。

当我们用 `g = Golem('Clay')` 这一句创建了一个 Golem 的 Instance 的时候，以下一连串的事情发生了：

> * `g` 从此之后就是一个根据 Golem 这个 Class 创建的 Instance，对使用者来说，它就是个 Object；
> * 因为 Golem 这个 Class 的代码中有 `__init__()`，所以，当 `g` 被创建的时候，`g` 就需要被初始化……
> * 在 `g` 所在的变量目录中，出现了一个叫做 `self` 的用来指代 `g` 本身的变量；
> * self.name 接收了一个参数，`'Clay'`，并将其保存了下来；
> * 生成了一个叫做 `self.built_year` 的变量，其中保存的是 `g` 这个 Object 被创建时的年份……

##### Inheritance

我们刚刚创建了一个 Golem Class，如果我们想用它 Inherit 一个新的 Class，比如，`Running_Golem`，一个能跑的机器人，那就像以下的代码那样做 —— 注意 `class Running_Golem` 之后的圆括号：


```python

class Golem:
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
    
    def say_hi(self):
        print('Hi!')

class Running_Golem(Golem): # 注意这个( )
    
    def run(self):
        print("Can't you see? I'm running...")

rg = Running_Golem('Clay')

rg.run
rg.run()
rg.name
rg.built_year
rg.say_hi()
```


    <bound method Running_Golem.run of <__main__.Running_Golem object at 0x0000028AB44B69A0>>

    Can't you see? I'm running...

    'Clay'


    2023

    Hi!


我们根据 Golem 这个 Class 创造了一个 Subclass —— `Running_Golem`，既然它是 Golem 的 Inheritance，那么 Golem 有的 Attributes 和 Methods 它都有，并且还多了一个 Method —— `self.run`。

##### Overrides

当我们创建一个 Inherited Class 的时候，可以重写（Overriding）Parent Class 中的 Methods。比如这样：


```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
import datetime

class Golem:
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
    
    def say_hi(self):
        print('Hi!')

class runningGolem(Golem):
    
    def run(self):
        print("Can't you see? I'm running...")
    
    def say_hi(self):                            # 不再使用 Parent Class 中的定义，而是新的……
        print('Hey! Nice day, Huh?')

rg = runningGolem('Clay')
rg.run
rg.run()
rg.name
rg.built_year
rg.say_hi()
```


    <bound method runningGolem.run of <__main__.runningGolem object at 0x0000024455954700>>


    Can't you see? I'm running...

    'Clay'

    2023


    Hey! Nice day, Huh?


##### Inspecting A Class

当我们作为用户想了解一个 Class 的 Interface，即，它的 Attributes 和 Methods 的时候，常用的有三种方式：

```python
1. help(object)
2. dir(object)
3. object.__dict__
```


```python
class Golem:
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
    
    def say_hi(self):
        print('Hi!')

class runningGolem(Golem):
    
    def run(self):
        print('Can\'t you see? I\'m running...')
    
    def say_hi(self):  # 不再使用 Parent Class 中的定义，而是新的……
        print('Hey! Nice day, Huh?')

rg = runningGolem('Clay')
help(rg)
dir(rg)
rg.__dict__
```

    Help on runningGolem in module __main__ object:
    
    class runningGolem(Golem)
     |  runningGolem(name=None)
     |  
     |  Method resolution order:
     |      runningGolem
     |      Golem
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  run(self)
     |  
     |  say_hi(self)
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from Golem:
     |  
     |  __init__(self, name=None)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from Golem:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)


    ['__class__',
     '__delattr__',
     '__dict__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__le__',
     '__lt__',
     '__module__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     '__weakref__',
     'built_year',
     'name',
     'run',
     'say_hi']


    {'name': 'Clay', 'built_year': 2023}

##### Scope

每个变量都属于某一个 **Scope**（变量的作用域），在同一个 Scope 中，变量可以被引用被操作

我们先给 Golem 这个 Class 增加一点功能 —— 我们需要随时知道究竟有多少个 Golem 处于活跃状态…… 也因此顺带给 Golem 加上一个 Method：`cease()`

另外，我们还要给机器人设置个使用年限，比如 10 年；

…… 而外部会每隔一段时间，用 `Golem.is_active()` 去检查所有的机器人，所以，不需要外部额外操作，到了年头，它应该能关掉自己

在运行以下代码之前，需要先介绍三个 Python 的内建函数：

> * `hasattr(object, attr)` 查询这个 `object` 中有没有这个 `attr`，返回布尔值
> * `getattr(object, attr)` 获取这个 `object` 中这个 `attr` 的值
> * `setattr(object, attr, value)` 将这个 `object` 中的 `attr` 值设置为 `value`


```python
class Golem:
    population = 0
    __life_span = 10
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
        self.__active = True
        Golem.population += 1   # 执行一遍之后，试试把这句改成 population += 1
    
    def say_hi(self):
        print('Hi!')
    
    def cease(self):
        self.__active = False
        Golem.population -= 1
    
    def is_active(self):
        if datetime.date.today().year - self.built_year >= Golem.__life_span:
            self.cease()
        return self.__active

g = Golem()
hasattr(Golem, 'population')      # True
hasattr(g, 'population')          # True
hasattr(Golem, '__life_span')     # False
hasattr(g, '__life_span')         # False
hasattr(g, '__active')            # False
Golem.population                  # 1
setattr(Golem, 'population', 10) 
Golem.population                  # 10
x = Golem()
Golem.population                  # 11
x.cease()
Golem.population                  # 10
getattr(g, 'population')          # 10
g.is_active()
```

如果你试过把第 13 行的 `Golem.population += 1` 改成 `population += 1`，你会被如下信息提醒：

```python
     12         self.__active = True
---> 13         population += 1
UnboundLocalError: local variable 'population' referenced before assignment
```
—— 本地变量 `population` 尚未赋值，就已经提前被引用…… 为什么会这样呢？因为在你所创建 `g` 之后，马上执行的是 `__init()__` 这个初始化函数，而 `population` 是在这个函数之外定义的……

如果你足够细心，你会发现这个版本中，有些变量前面有两个下划线 `__`，比如，`__life_span` 和 `self.__active`。**这是 Python 的定义，变量名前面加上一个以上下划线（Underscore）`_` 的话，那么该变量是 “私有变量”（Private Variables），不能被外部引用**。而按照 Python 的惯例，我们会使用两个下划线起始，去命名私有变量，如：`__life_span`。你可以回去试试，把所有的 `__life_span` 改成 `_life_span`（即，变量名开头只有一个 `_`，那么，`hasattr(Golem, '_life_span')` 和 `hasattr(g, '_life_span')` 的返回值就都变成了 `True`。


**补充**

在本例子中，在 `__init__(self, name=None)` 函数中 `self.population` 和 `Golem.population` 都可以使用，但使用效果是不一样的：
> * `self.population` 总是去读取 `Golem` 类中 `population` 的初始值，即使后面通过 `setattr(Golem, 'population', 10)` 更改 `population` 的值后，`self.population` 的值仍为 `0`，但 `Golem.population` 值则为 `10`，你可以自己动手尝试一下。

##### Encapsulation

到目前为止，Golem 这个 Class 看起来不错，但有个问题，它里面的数据，外面是可以随便改的 —— 虽然，我们已经通过给变量 life_span 前面加上两个下划线，变成 `__life_span`，使其成为私有变量，外部不能触达（你不能引用 `Golem.__life_span`），可 Golem.population 就不一样，外面随时可以引用，还可以随时修改它，只需要写上一句：

```python
Golem.population = 1000000
```

我们干脆把 `population` 这个变量也改成私有的罢：`__population`，而后需要从外界查看这个变量的话，就在 Class 里面写个函数，返回那个值好了：


```python
class Golem:
    __population = 0
    __life_span = 10
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
        self.__active = True
        Golem.__population += 1
    
    def say_hi(self):
        print('Hi!')
    
    def cease(self):
        self.__active = False
        Golem.__population -= 1
    
    def is_active(self):
        if datetime.date.today().year - self.built_year >= Golem.__life_span:
            self.cease
        return self.__active
    
    def population(self):
        return Golem.__population

g = Golem('Clay')
g.population
print("---------------------")
g.population()
```


    <bound method Golem.population of <__main__.Golem object at 0x0000028AB5543460>>

    ----------------------

    1

如果，你希望外部能够像获得 Class 的属性那样，直接写 `g.population`，而不是必须加上一个括号 `g.population()` 传递参数（实际上传递了一个隐含的 `self` 参数），那么可以在 `def population(self):` 之前的一行加上一句 `@property`：

```python
class Golem:
    __population = 0
    ...
    
    @property
    def population(self):
        return Golem.__population
```

如此这般之后，你就可以用 `g.population` 了：


```python
class Golem:
    __population = 0
    __life_span = 10
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
        self.__active = True
        Golem.__population += 1
    
    def say_hi(self):
        print('Hi!')
    
    def cease(self):
        self.__active = False
        Golem.__population -= 1
    
    def is_active(self):
        if datetime.date.today().year - self.built_year >= Golem.__life_span:
            self.cease
        return self.__active
    
    @property
    def population(self):
        return Golem.__population

g = Golem('Clay')
g.population
# g.population = 100
```


    1


如此这般之后，不仅你可以直接引用 `g.population`，并且，在外部不能再直接给 `g.population` 赋值了，否则会报错：

```python
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-16-5d8c475304d3> in <module>
     26 g = Golem('Clay')
     27 g.population
---> 28 g.population = 100

AttributeError: can't set attribute
```

到此为止，Encapsulation 就做得不错了。

如果你非得希望从外部可以设置这个值，那么，你就得再写个函数，并且在函数之前加上一句：
```python
    ...
    
    @property
    def population(self):
        return Golem.__population
    
    @population.setter
    def population(self, value):
        Golem.__population = value

```

这样之后，`.population` 这个 Attribute 就可以从外部被设定其值了（虽然在当前的例子中显得没必要让外部设定 `__population` 这个值…… 以下仅仅是为了举例）：


```python
class Golem:
    __population = 0
    __life_span = 10
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
        self.__active = True
        Golem.__population += 1
    
    def say_hi(self):
        print('Hi!')
    
    def cease(self):
        self.__active = False
        Golem.__population -= 1
    
    def is_active(self):
        if datetime.date.today().year - self.built_year >= Golem.__life_span:
            self.cease
        return self.__active
    
    @property
    def population(self):
        return Golem.__population
    
    @population.setter
    def population(self, value):
        Golem.__population = value

g = Golem('Clay')
g.population
g.population = 100
ga = Golem('New')
g.population
ga.population
help(Golem)
Golem.__dict__
g.__dict__
hasattr(Golem, 'population')
getattr(Golem, 'population')
setattr(Golem, 'population', 10000)
g.population    # 所以，在很多的情况下，不把数据封装在 Class 内部的话，后面会有很多麻烦。
```


    1

    101

    101


    Help on class Golem in module __main__:
    
    class Golem(builtins.object)
     |  Golem(name=None)
     |  
     |  Methods defined here:
     |  
     |  __init__(self, name=None)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  cease(self)
     |  
     |  is_active(self)
     |  
     |  say_hi(self)
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
     |  
     |  population


    mappingproxy({'__module__': '__main__',
                  '_Golem__population': 101,
                  '_Golem__life_span': 10,
                  '__init__': <function __main__.Golem.__init__(self, name=None)>,
                  'say_hi': <function __main__.Golem.say_hi(self)>,
                  'cease': <function __main__.Golem.cease(self)>,
                  'is_active': <function __main__.Golem.is_active(self)>,
                  'population': <property at 0x2445599cd10>,
                  '__dict__': <attribute '__dict__' of 'Golem' objects>,
                  '__weakref__': <attribute '__weakref__' of 'Golem' objects>,
                  '__doc__': None})

    {'name': 'Clay', 'built_year': 2023, '_Golem__active': True}

    True

    <property at 0x2445599cd10>

    10000

