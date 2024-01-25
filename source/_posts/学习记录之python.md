---
title: 学习记录之python
date: 2024-01-25 21:56:25
tags: python
---

# 1 入

```python
print('Hello World!')
```

python可视化：pythontutor.com



## 1.1 注释

+ 单行注释 #

+ 多行注释 ''' """

  ```python
  # 这是单行注释
  '''
  多行注释
  '''
  """
  多行注释
  """
  ```

## 1.2 拷贝

+ 浅拷贝（Shallow Copy）：浅拷贝创建一个新的对象，但是它只复制了原始对象中的引用。也就是说，新对象和原始对象**共享相同的数据**。浅拷贝通常适用于简单的数据结构，如列表、字典等。（一个修改了，另一个也修改了）

  ```python
  import copy
  
  # 列表的浅拷贝
  list1 = [1, 2, 3]
  list2 = copy.copy(list1)
  print(list2)  # 输出 [1, 2, 3]
  
  # 字典的浅拷贝
  dict1 = {'name': 'Alice', 'age': 20}
  dict2 = copy.copy(dict1)
  print(dict2)  # 输出 {'name': 'Alice', 'age': 20}
  ```

+ 深拷贝（Deep Copy）：深拷贝创建一个完全独立的新对象，并且递归地复制原始对象及其所有嵌套的对象。深拷贝在处理复杂的数据结构时非常有用，如嵌套的列表、字典等。

  ```python
  import copy
  
  # 列表的深拷贝
  list1 = [1, 2, [3, 4]]
  list2 = copy.deepcopy(list1)
  print(list2)  # 输出 [1, 2, [3, 4]]
  
  # 字典的深拷贝
  dict1 = {'name': 'Alice', 'info': {'age': 20}}
  dict2 = copy.deepcopy(dict1)
  print(dict2)  # 输出 {'name': 'Alice', 'info': {'age': 20}}
  ```

  

# 2 变量

无需定义变量类型

```python
name = "chichu"
age = 18
num = 4.3
a, b = 23, 4.2
```

输出

```python
print(name1, name2) # 默认空格分隔
print(name1, name2, sep = '$$')  # 分隔是$$
print(name1, name2, end='333') # 默认结尾'\n'
```

## 2.1 变量类型

+ Number 数字

  + int float bool

  ```python
  a = 1, b = 2, bool = True
  ```

+ String 

  ```python
  str1 = 'H1'
  str2 = '''
  duoduo
  shaos
  '''
  ```

  

+ List 列表

+ Tuple 元组

+ Dict 字典

+ Set 集合

## 2.2 输入

input 函数

```python
name = input('请输入您的姓名：')
print(f'Hello, {name}!')
```

## 2.3 强制类型转化

+ 整形转化

  ```python
  x = int(3.14)  # 将浮点型转换为整型，结果为 3
  y = int('123')  # 将字符串转换为整型，结果为 123
  ```

+ 浮点型转化

  ```
  x = float(3)  # 将整型转换为浮点型，结果为 3.0
  y = float('3.14')  # 将字符串转换为浮点型，结果为 3.14
  ```

+ 字符串

  ```python
  x = str(123)  # 将整型转换为字符串，结果为 '123'
  y = str(3.14)  # 将浮点型转换为字符串，结果为 '3.14'
  ```


+ 列表

  ```python
  str1 = 'hello1'
  print(list(str1)) # ['h', 'e', 'l', 'l', 'o', '1']
  ```

  

## 2.4 隐式转换

+ 整形浮点型

  ```python
  a = 10
  b = 3.14
  c = a + b  # a 会被自动转换为 10.0，结果为 13.14
  ```

+ 字符串与数字型

  ```python
  a = '10'
  b = 3.14
  c = a + b  # a 会被自动转换为整型，结果为 13.14
  ```

+ 布尔型与整型

  ```python
  a = True
  b = 3
  c = a + b  # True 会被自动转换为整型 1，结果为 4
  ```

# 3 运算

## 3.1 算术运算

| 运算符 | 描述                 |
| ------ | -------------------- |
| +      | 加法                 |
| -      | 减法                 |
| *      | 乘法                 |
| /      | 除法                 |
| %      | 取余                 |
| **     | 幂运算               |
| //     | 整数除法（向下取整） |

==python中没有a++，a--==

## 3.2 关系运算符

| 运算符 | 描述                               |
| ------ | ---------------------------------- |
| ==     | 检查两个值是否相等                 |
| !=     | 检查两个值是否不相等               |
| >      | 检查左操作数是否大于右操作数       |
| <      | 检查左操作数是否小于右操作数       |
| >=     | 检查左操作数是否大于或等于右操作数 |
| <=     | 检查左操作数是否小于或等于右操作数 |

## 3.3 成员运算符

| 运算符 | 描述                                                       |
| ------ | ---------------------------------------------------------- |
| in     | 如果在序列中找到具有相应值的项，则为 True                  |
| not in | 如果在序列中没有找到具有相应值的项，则为 True              |
| is     | 判断两个变量是否引用了同一个对象（通常用于判断 None 变量） |
| is not | 判断两个变量是否没有引用同一个对象                         |

```python
# 检查元素是否在列表中
fruits = ["apple", "banana", "cherry"]
print("apple" in fruits)  # 输出 True

# 检查键是否在字典中
ages = {"Tom": 18, "Jack": 20, "Mary": 22}
print("Tom" in ages)  # 输出 True
print("John" not in ages)  # 输出 True

# 检查变量是否为 None
x = None
print(x is None)  # 输出 True

```

## 3.4 逻辑运算符

| 运算符 | 描述                                                 |
| ------ | ---------------------------------------------------- |
| and    | 如果两个操作数都为 True，则计算结果为 True           |
| or     | 如果两个操作数中有任意一个为 True，则计算结果为 True |
| not    | 取反操作，如果操作数为 True，则返回 False            |

```python
# and 运算符，例如判断数值是否在指定范围内
x = 5
print(x > 0 and x < 10)  # 输出 True

# or 运算符，例如判断字符串是否包含某个字符
text = "Hello, world!"
print("e" in text or "a" in text)  # 输出 True

# not 运算符，例如取反操作
is_valid = True
print(not is_valid)  # 输出 False

```

# 4 分支循环

## 4.1 分支结构

```python
score = 75
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'F'
print("成绩等级是：", grade)
```

## 4.2 循环

```python
count = 0

while count < 5:
    print("当前计数: ", count)
    count += 1

print("循环结束")

```

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits):
    print(index, fruit)

for i in range(5): # 0 ~ 4
    print(i)
for i in range(1, 6) # 1 ~ 5
```

# 5 字符串

+ 外面使用单引号，内部屏蔽单引号，双引号同理
+ 转义字符

- \\`：反斜杠（用于表示反斜杠字符）。
- `\'`：单引号（用于表示单引号字符）。
- `\"`：双引号（用于表示双引号字符）。
- `\n`：换行符（将光标移到下一行的开头位置）。
- `\r`：回车符（将光标移到当前行的开头位置）。
- `\t`：制表符（在输出中创建水平制表或跳到下一个制表位置）。
- `\b`：退格符（将光标向左移动一个位置）。
- `\f`：换页符（在输出中创建一个新页）。

加上r开头无视制表符

## 5.1 格式化输出

```python
name = "cc"
print(f"my name is {name}")
```

```python
name = "John"
age = 25
print("My name is %s and I am %d years old." % (name, age))
```

```python
name = "John"
age = 25
print("My name is {} and I am {} years old.".format(name, age))
```

## 5.2 操作

+ 下标访问

  ```python
  text = "Hello, World!"
  print(text[0])  # 访问第一个字符
  print(text[7])  # 访问第八个字符
  print(text[-1])  # 访问最后一个字符
  print(text[-6])  # 访问倒数第六个字符
  ```

+ 切片

  `[start:stop:step]` 格式，其中：

  - `start` 是起始索引（默认为 0）
  - `stop` 是结束索引（不包含在切片结果中）
  - `step` 是步长（默认为 1）

  ```python
  text = "Hello, World!"
  print(text[7:12])   # 提取索引从7到11的字符
  print(text[-6:-1])    # 提取倒数第六个到倒数第二个字符
  
  my_list = [1, 2, 3, 4, 5]
  print(my_list[1:4])  # 提取索引从1到3的元素
  print(my_list[::-1])  # 逆序提取所有元素
  
  my_tuple = ('apple', 'banana', 'cherry', 'date')
  print(my_tuple[::2])  # 按照步长为2提取所有元素
  print(my_tuple[-2:-5:-1])  # 逆序提取倒数第二到倒数第四个元素
  
  ```

+ 操作函数

  1. `len(string)`：返回字符串的长度。

  2. `string.lower()`：将字符串中的字符转换为小写形式。

  3. `string.upper()`：将字符串中的字符转换为大写形式。

  4. `string.capitalize()`：将字符串的首字母转换为大写形式，其余字符转换为小写形式。

  5. `string.title()`：将字符串中每个单词的首字母转换为大写形式，其余字符转换为小写形式。

  6. `string.strip()`：去除字符串开头和结尾的空格或指定字符。

  7. `string.split(sep)`：根据分隔符 `sep` 将字符串拆分成子字符串，并返回一个列表。

  8. `string.join(iterable)`：将可迭代对象 `iterable` 中的字符串元素连接起来，中间使用 `string` 分隔。

     ```python
     string = "-"
     my_list = ["apple", "banana", "cherry"]
     result = string.join(my_list)
     print(result)
      # apple-banana-cherry
     ```

  9. `string.replace(old, new)`：将字符串中的所有匹配 `old` 的子串替换为 `new`。

  10. `string.startswith(prefix)`：检查字符串是否以指定的前缀 `prefix` 开头，返回布尔值。

  11. `string.endswith(suffix)`：检查字符串是否以指定的后缀 `suffix` 结尾，返回布尔值。

  12. `string.find(substring)`：在字符串中查找子串 `substring` 的第一个匹配位置，并返回索引值。

  13. `string.count(substring)`：统计字符串中子串 `substring` 出现的次数。

  14. `string.isalpha()`：检查字符串是否只包含字母字符。

  15. `string.isdigit()`：检查字符串是否只包含数字字符。

## 5.3 编码解码

```python
# 编码示例
string = "你好，世界！"  # 普通字符串
byte_string = string.encode("utf-8")  # 编码为字节字符串
print(byte_string)  # 输出：b'\xe4\xbd\xa0\xe5\xa5\xbd\xef\xbc\x8c\xe4\xb8\x96\xe7\x95\x8c\xef\xbc\x81'

# 解码示例
decoded_string = byte_string.decode("utf-8")  # 解码为普通字符串
print(decoded_string)  # 输出：你好，世界！
```

## 5.4 ASCII 转换

```python
# ASCII 码转字符示例
ascii_value = 65  # ASCII 码值
character = chr(ascii_value)  # 转换为字符
print(character)  # 输出：A

# 字符转 ASCII 码示例
character = 'A'  # 字符
ascii_value = ord(character)  # 转换为 ASCII 码值
print(ascii_value)  # 输出：65
```

# 6 列表

## 6.1 特征

+ 有序性：列表中的元素按照它们在列表中的位置顺序进行存储和访问，可以通过索引来访问和修改特定位置的元素。索引从 0 开始，第一个元素的索引为 0，第二个元素的索引为 1，依此类推。
+ 可变性：列表中的元素可以随时被修改、替换或删除，也可以在任意位置插入新元素。这意味着列表的长度和内容都是可变的。
+ 可重复性：列表中可以包含重复的元素，即同一个值可以出现多次。
+ 多样性：列表可以容纳不同类型的元素，例如整数、浮点数、字符串、布尔值等。

## 6.2 常见操作

创建列表：

```python
empty_list = []  # 创建一个空列表
my_list = [1, 2, 3, 'a', 'b', 'c']  # 创建一个包含元素的列表
```

访问和修改元素：

```python
my_list = ['a', 'b', 'c']
print(my_list[0])  # 输出：'a'
my_list[1] = 'd'
print(my_list)  # 输出：['a', 'd', 'c']
```

添加元素：

```python
my_list = ['a', 'b', 'c']
my_list.append('d')
print(my_list)  # 输出：['a', 'b', 'c', 'd']

# 如果直接append列表，就变成二维列表了
list1 = my_list.copy()
list1.append([23,43]) # ['a', 'b', 'c', 'd', [23, 43]]

# 选择extend会进行一次拆分
list2 = my_list.copy()
list2.extend(["34", "34"]) # 等价于list2 += ["34", "34"], ['a', 'b', 'c', 'd', '34', '34']
list2.extend("qqqe") # ['a', 'b', 'c', 'd', '34', '34']

my_list = [1, 2, 3, 4]
my_list.insert(2, 5)
print(my_list) # [1, 2, 5, 3, 4]
```

删除元素：

```python
my_list = ['a', 'b', 'c']
del my_list[1]  # 删除索引为1的元素
print(my_list)  # 输出：['a', 'c']

my_list.remove('a')  # 删除值为'a'的元素
print(my_list)  # 输出：['c']
my_list.pop(0)  # 删除索引0的位置的元素，无参数是删除最后一个
my_list.clear()  # 清空
```

切片操作：

```python
my_list = [1, 2, 3, 4, 5]
sub_list = my_list[1:3]  # 获取索引为1到2的子列表
print(sub_list)  # 输出：[2, 3]
```

列表长度：

```python
my_list = [1, 2, 3, 4, 5]
length = len(my_list)
print(length)  # 输出：5
```

其他操作：

```python
my_list.reverse()  # 反转列表元素
print(my_list)  # 输出：[5, 4, 3, 2, 1]

another_list = [6, 7, 8]
my_list.extend(another_list)  # 将另一个列表的元素添加到当前列表
print(my_list)  # 输出：[5, 4, 3, 2, 1, 6, 7, 8]

count = my_list.count(5)  # 统计5在列表中出现的次数
print(count)  # 输出：1
```

遍历：

```python
my_list = ['a', 'b', 'c']

for index, value in enumerate(my_list): # 获取索引和元素
    print(index, value)
```

排序：

````python
my_list = [3, 1, 4, 2, 5]
my_list.sort()  # 对列表进行升序排序
my_list.sort(reverse=True)  # 进行降序
print(my_list)  # 输出：[1, 2, 3, 4, 5]，对本身列表进行改变

# sorted(iterable, key=None, reverse=False)
list1 = sorted(my_list)  # 生成新的列表
list1 = sorted(my_list, reverse=True)  # 降序

my_list = ['apple', 'banana', 'cherry', 'date']
sorted_list = sorted(my_list, key=len)

print(sorted_list)  # ['date', 'apple', 'cherry', 'banana']
````

列表生成：

```python
list1 = [None] * 10

list2 = list(range(1, 11))

list3 = [i * 2 for i in range(1, 6)]
```

# 7 字典

```python
person = {
    "name": "Alice",
    "age": 27,
    "city": "Beijing"
}
print(person["name"])  # 访问键为"name"的值："Alice"
person["age"] = 28  # 修改键为"age"的值为28
print(person)  # 打印整个字典：{'name': 'Alice', 'age': 28, 'city': 'Beijing'}

person["email"] = "alice@example.com"  # 添加新的键值对
print(person)  # 打印整个字典，包含新的键值对：{'name': 'Alice', 'age': 28, 'city': 'Beijing', 'email': 'alice@example.com'}

del person["city"]  # 删除键为"city"的键值对
print(person)  # 打印整个字典，不再包含"city"键值对：{'name': 'Alice', 'age': 28, 'email': 'alice@example.com'}

length = len(person)  # 获取字典的长度
print(length)  # 打印字典长度：3
```

```python
person.key()  # 所有的键
person.value()  # 所有的键值
person.item()  # 所有的项
for i in person:  # 遍历所有的key()
	print(i)
for key, value in enumerate(person):  # 带下标的key
	print(key, value)
for key, value in person.items():  # 遍历所有
	print(key, value)
for v in person.value()  # 遍历键值
	print(v)

  # 合并
dict1 = {"name": "Alice", "age": 27}
dict2 = {"city": "Beijing", "email": "alice@example.com"}

dict1.update(dict2)  # 合并字典

print(dict1)  # 打印合并后的字典：{'name': 'Alice', 'age': 27, 'city': 'Beijing', 'email': 'alice@example.com'}

```

# 8 集合

1. 无序性：集合中的元素没有固定的顺序，每次输出的顺序可能不同。
2. 唯一性：集合中的元素是唯一的，不允许有重复的元素。
3. 可变性：集合是可变的，可以通过添加或删除元素来修改集合。
4. 集合元素必须是可哈希的：集合中的元素必须是可哈希的，即不可变的（例如数字、字符串、元组），但不支持可变类型（例如列表、字典）。
5. 数学操作：可以进行集合间的数学操作，如并集、交集和差集等。

```python
# 创建集合
set1 = {1, 2, 3}
set2 = set([3, 4, 5])

# 添加元素
set1.add(4)
print(set1)  # 输出 {1, 2, 3, 4}

# 删除元素
set2.remove(4)
print(set2)  # 输出 {3, 5}

# 集合运算
union_set = set1.union(set2)  # 并集
intersection_set = set1.intersection(set2)  # 交集
difference_set = set1.difference(set2)  # 差集
print(union_set)  # 输出 {1, 2, 3, 5}
print(intersection_set)  # 输出 {3}
print(difference_set)  # 输出 {1, 2, 4}

```

# 9 元组

1. 有序性：元组中的元素按照定义的顺序排列，并且保持不变。
2. 不可变性：元组的元素不能被修改，添加或删除。一旦创建，元组的内容就不可更改。
3. 支持多种数据类型：元组可以包含不同类型的数据，例如整数、浮点数、字符串等。
4. 可用于索引和切片：可以使用索引和切片操作访问元组中的元素。

```python
# 创建元组
tuple1 = (1, 2, 3)
tuple2 = tuple([4, 5, 6])

# 访问元素
print(tuple1[0])  # 输出 1
print(tuple2[1:])  # 输出 (5, 6)

# 元组拼接
tuple3 = tuple1 + tuple2
print(tuple3)  # 输出 (1, 2, 3, 4, 5, 6)

# 元组解包
a, b, c = tuple1
print(a, b, c)  # 输出 1 2 3

# 遍历元组
for item in tuple2:
    print(item)  # 输出 4 5 6

```

+ 需要注意的是，元组是不可变的，这意味着一旦创建，就不能修改元组中的元素。如果需要修改元素，可以将元组转换为列表进行修改，然后再转换回元组。

```python
tuple4 = (1, 2, 3)
list4 = list(tuple4)
list4[0] = 4
tuple4 = tuple(list4)
print(tuple4)  # 输出 (4, 2, 3)
```

# 10 函数

## 10.1 基本调用

定义函数：使用 `def` 关键字来定义一个函数，并给函数取一个名称。函数名称后面跟着一对圆括号 `()`，括号中可以包含参数（可选），参数用于接收传递给函数的值。函数体以冒号 `:` 开始，并通过缩进来表示函数体内的代码块。

```python
def greet():
    print("Hello, world!")

def add(a, b):
    return a + b

```

调用函数：当需要执行函数内的代码时，通过函数名称后跟一对圆括号 `()` 来调用函数。如果函数有参数，需要在括号中传递相应的值。

```python
greet()  # 调用 greet 函数，输出 "Hello, world!"

result = add(3, 5)  # 调用 add 函数，并将返回值赋给 result 变量
print(result)  # 输出 8
```

## 10.2 参数

+ 默认参数

  ```python
  def greet(name, greeting="Hello"):
      """
      给定名称和问候语，打印出个性化的问候信息。
      
      Args:
          name (str): 要问候的人的名称。
          greeting (str, optional): 问候语，默认为"Hello"。
      """
      message = f"{greeting}, {name}!"
      print(message)
  
  # 不指定 greeting 参数的值，默认使用 "Hello"
  greet("Alice")  # 输出：Hello, Alice!
  
  # 传递自定义的 greeting 参数值
  greet("Bob", "Hi")  # 输出：Hi, Bob!
  ```

+ 不定长参数

  ```python
  def my_func(*args):
      """
      接收任意数量的位置参数，并打印出来。
      
      Args:
          *args: 任意数量的位置参数。
      """
      for arg in args:
          print(arg)
  
  # 调用函数并传递不同数量的位置参数
  my_func(1, 2, 3)               # 输出：1 2 3
  my_func('Hello', 'World')      # 输出：Hello World
  my_func('a', 'b', 'c', 'd')    # 输出：a b c d
  ```

  ```python
  def my_func(**kwargs):
      """
      接收任意数量的关键字参数，并打印出来。
      
      Args:
          **kwargs: 任意数量的关键字参数。
      """
      for key, value in kwargs.items():
          print(f"{key}: {value}")
  
  # 调用函数并传递不同的关键字参数
  my_func(name='Alice', age=25)          # 输出：name: Alice, age: 25
  my_func(city='New York', country='USA')# 输出：city: New York, country: USA
  ```

+ 匿名函数

  ```python
  square = lambda x: x**2
  
  print(square(4))  # 输出：16
  print(square(7))  # 输出：49
  
  ```

  

+ 回调函数

  回调函数（Callback Function）是一种将函数作为参数传递给另一个函数，并在特定事件发生时被调用的函数。在 Python 中，可以使用回调函数来实现异步操作、事件处理、回调机制等。

  ```python
  def process_data(data, callback):
      # 在处理数据之后，调用回调函数
      result = data * 2
      callback(result)
  
  def handle_result(result):
      # 处理回调函数的结果
      print("处理结果:", result)
  
  data = 5
  process_data(data, handle_result)
  ```

  

+ 闭包函数

  闭包函数（Closure Function）是指在一个函数内部定义并使用了另一个函数，并且这个内部函数可以访问外部函数中的变量。换句话说，闭包函数可以捕获并存储其所在作用域的状态。

  Python 中的闭包函数是一种非常有用的功能，它可以帮助我们实现某些高级的编程技巧和模式，例如装饰器、工厂函数等。闭包函数的特点是：

  1. 内部函数可以访问外部函数定义的变量：闭包函数中的内部函数可以引用并访问外部函数中的变量，即使外部函数已经执行完毕，内部函数仍然可以访问到那些变量。
  2. 外部函数可以返回内部函数作为结果：外部函数可以返回其内部函数作为结果，使得内部函数在外部函数执行完毕后仍然可以被调用。

  ```python
  def outer_function(x):
      def inner_function(y):
          return x + y
      return inner_function
  
  closure = outer_function(5)  # 感觉这里返回的是这个函数的内函数
  result = closure(3)
  print(result)  # 输出 8
  ```

  

## 10.3 使用全局变量

+ 直接使用即可，但是局部变量不会改变全局变量的值

+ **global**

```
x = 10  # 全局变量

def func():
    global x  # 声明 x 是全局变量
    x = 20   # 修改全局变量 x 的值

print("Before calling func:", x)  # 输出：Before calling func: 10
func()
print("After calling func:", x)   # 输出：After calling func: 20

```

## 10.4 filter筛选函数

`filter(function, iterable)`

其中，`function` 是一个判断函数，用于指定筛选的条件；`iterable` 是一个可迭代对象，包含需要筛选的元素。

`filter()` 函数将会返回一个 `filter` 对象，它是一个迭代器，可以通过遍历或转换为其他序列（如列表）来获取结果。在筛选过程中，只有满足 `function` 函数返回值为 `True` 的元素会被保留。

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

def is_even(x):
    return x % 2 == 0

result = filter(is_even, numbers)

print(list(result))  # 输出：[2, 4, 6, 8, 10]

```

## 10.5 map()函数

`map(function, iterable)`

其中，`function` 是一个函数，用于对每个元素进行处理；`iterable` 是一个可迭代对象，包含需要处理的元素。

`map()` 函数将会返回一个 `map` 对象，它是一个迭代器，可以通过遍历或转换为其他序列（如列表）来获取结果。在处理过程中，会将 `iterable` 中的每个元素依次传递给 `function` 函数进行处理，并将处理后的结果保存在 `map` 对象中。

```python
numbers = [1, 2, 3, 4, 5]

result = map(lambda x: x ** 2, numbers)

print(list(result))  # 输出：[1, 4, 9, 16, 25]
```

## 10.6 装饰器函数

装饰器函数通常采用一个函数作为输入参数，并返回一个新的函数作为输出结果。这样，我们可以使用装饰器函数来包装（decorate）其他函数，以添加一些额外的功能、修改其行为或执行其他操作。（相当于优雅地修改其他函数）

```python
def decorator_function(original_function):
    def wrapper_function():
        # 在调用原始函数之前执行一些操作
        print("执行装饰器添加的功能")
        
        # 调用原始函数
        original_function()
        
        # 在调用原始函数之后执行一些操作
        print("装饰器功能执行完毕")
    
    # 返回包装后的函数对象
    return wrapper_function

def greet():
    print("Hello, world!")

# 使用装饰器函数来装饰 greet() 函数
greet = decorator_function(greet)

# 执行装饰后的函数
greet()

```

```python
def decorator_function(original_function):
    def wrapper_function():
        print("执行装饰器添加的功能")
        original_function()
        print("装饰器功能执行完毕")
    return wrapper_function

@decorator_function
def greet():
    print("Hello, world!")

greet()
```

# 11 模块

## 11.1 模块基本操作

```python
# 导入整个模块
import math

# 使用模块中的函数
print(math.sqrt(16))  # 输出：4.0

# 导入模块并指定别名
import datetime as dt

# 使用别名调用模块中的类
today = dt.date.today()
print(today)  # 输出当前日期

# 导入模块中的特定成员（函数、类、变量等）
from random import randint

# 直接使用成员，无需再加模块前缀
print(randint(1, 10))  # 输出一个随机整数

# 导入模块中的所有成员（函数、类、变量等）
from statistics import *

# 直接使用所有成员，无需再加模块前缀
data = [1, 2, 3, 4, 5]
print(mean(data))  # 输出平均值
```

## 11. 2 os模块

1. 文件和目录操作：
   - 创建目录：`os.mkdir(path)`
   - 删除目录：`os.rmdir(path)`
   - 列出目录下的文件和子目录：`os.listdir(path)`
   - 获取当前工作目录：`os.getcwd()`
   - 改变当前工作目录：`os.chdir(path)`

- 重命名文件或目录：`os.rename(src, dst)`
- 删除文件：`os.remove(path)`
- 检查文件是否存在：`os.path.exists(path)`
- 检查是否为目录：`os.path.isdir(path)`
- 检查是否为文件：`os.path.isfile(path)`
- 获取文件大小：`os.path.getsize(path)`
- 复制文件：可以使用`shutil`模块中的`shutil.copy(src, dst)`进行文件复制操作。

- 使用`os.system(command)`执行系统命令。例如：`os.system("ls")`会在终端运行`ls`命令。

## 11.3 random模块

`random.random()`： 返回一个0到1之间（包括0但不包括1）的随机浮点数。

```python
import random

num = random.random()
print(num)
# 输出：0.123456789 （随机的0到1之间的浮点数）

```

`random.randint(a, b)`： 返回一个指定范围内的随机整数，包括边界值`a`和`b`。 

```python
import random

num = random.randint(1, 10)
print(num)
# 输出：4 （随机的1到10之间的整数）
```

`random.choice(seq)`： 从一个非空序列中随机选择一个元素，并返回。

```python
import random

fruits = ['apple', 'banana', 'orange']
choice = random.choice(fruits)
print(choice)
# 输出：'banana' （随机选择一个水果）
```

`random.shuffle(seq)`： 将一个序列中的元素随机打乱顺序，改变原序列，没有返回值。

```python
import random

numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)
print(numbers)
# 输出类似于：[4, 2, 5, 1, 3] （随机打乱元素顺序）

```

`random.sample(population, k)`： 从给定的序列中随机选择`k`个元素并返回，不改变原序列。

```python
import random

numbers = [1, 2, 3, 4, 5]
sample = random.sample(numbers, 3)
print(sample)
# 输出类似于：[4, 2, 5] （随机选择3个元素）

```

## 11. 4 datetime模块

`datetime.datetime.now()`： 返回当前的日期和时间。

```python
import datetime

now = datetime.datetime.now()
print(now)
# 输出类似于：2023-07-13 11:46:28.123456 （当前的日期和时间）

```

`datetime.datetime(year, month, day[, hour[, minute[, second[, microsecond[, tzinfo]]]]])`： 创建一个表示指定日期和时间的`datetime`对象。

```python
import datetime

dt = datetime.datetime(2023, 7, 13, 12, 30)
print(dt)
# 输出：2023-07-13 12:30:00 （表示指定日期和时间的datetime对象）

```

`datetime.timedelta(days[, seconds[, microseconds[, milliseconds[, minutes[, hours[, weeks]]]]]])`： 表示时间间隔的类，可以用于进行日期和时间的计算。

```python
import datetime

delta = datetime.timedelta(days=7)
one_week_later = datetime.datetime.now() + delta
print(one_week_later)
# 输出：2023-07-20 11:46:28.123456 （当前时间的一周后）

```

`datetime.strftime(format)`与`datetime.strptime(date_string, format)`： `strftime`方法将`datetime`对象格式化为字符串，而`strptime`方法将字符串解析为`datetime`对象。

```python
import datetime

dt = datetime.datetime.now()
dt_str = dt.strftime('%Y-%m-%d %H:%M:%S')
print(dt_str)
# 输出类似于：2023-07-13 11:46:28 （将datetime对象格式化为字符串）

dt_parsed = datetime.datetime.strptime('2023-07-13 12:30:00', '%Y-%m-%d %H:%M:%S')
print(dt_parsed)
# 输出：2023-07-13 12:30:00 （将字符串解析为datetime对象）

```

## 11. 5 time模块

`time.time()`： 返回当前时间的时间戳（自新纪元以来的秒数）。

```python
import time

timestamp = time.time()
print(timestamp)
# 输出类似于：1626162382.123456 （当前时间的时间戳）

```

`time.sleep(secs)`： 让程序暂停执行指定的秒数。

```python
import time

print('开始')
time.sleep(3)
print('结束')
# 输出：
# 开始
# （3秒后）
# 结束

```

`time.strftime(format[, t])`与`time.strptime(string[, format])`： `strftime`方法将时间元组或struct_time对象格式化为字符串，`strptime`方法将字符串解析为时间元组对象。

```python
import time

timestamp = time.time()
time_str = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(timestamp))
print(time_str)
# 输出类似于：2023-07-13 11:46:28 （将时间戳格式化为字符串）

time_parsed = time.strptime('2023-07-13 12:30:00', '%Y-%m-%d %H:%M:%S')
print(time_parsed)
# 输出类似于：time.struct_time(tm_year=2023, tm_mon=7, tm_mday=13, tm_hour=12, tm_min=30, tm_sec=0, tm_wday=3, tm_yday=194, tm_isdst=-1) （将字符串解析为时间元组对象）

```

# 12 类

## 12.1 初始化类

定义类（Class）：类是面向对象编程的基础，通过定义类来创建新的对象。类定义了对象的属性和方法。可以使用 `class` 关键字来定义一个类。

构造函数 `__init__()` 在创建对象时被调用，用于初始化对象的属性。它是一个特殊的方法，以双下划线开头和结尾。可以在构造函数中定义对象的初始状态。

析构函数 `__del__()` 在对象被销毁时自动调用。它也是一个特殊的方法，以双下划线开头和结尾。析构函数可以用于释放资源或执行清理操作。

`Person` 类的析构函数 `__del__()` 会在对象被销毁时自动调用。使用 `del` 关键字可以手动销毁对象。

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print("Person object created.")

    def __del__(self):
        print("Person object destroyed.")

person = Person("Alice", 25)

del person

```

## 12.2 类属性和对象属性

类属性是定义在类中的变量，被所有该类的实例共享。它们属于类本身，而不属于类的任何特定实例。可以通过类名或实例访问类属性。

对象属性是定义在类实例中的变量，每个实例都拥有自己的一组对象属性。它们可以在类的构造函数中初始化，并使用 `self` 关键字绑定到对象。

需要注意的是，对象属性和类属性可以具有相同的名称，但它们是不同的。**当通过实例访问属性时，如果实例没有该属性，则会查找类属性。**

```python
class Person:
    species = "Human"

    def __init__(self, name):
        self.name = name

# 创建实例并访问属性
person = Person("Alice")
print(person.species)  # 输出: Human
print(person.name)  # 输出: Alice

# 修改类属性不影响已创建的实例
Person.species = "Homo sapiens"
print(person.species)  # 输出: Homo sapiens

```

## 12.3 继承

要创建一个继承关系，需要在定义子类时将父类作为参数传递给子类。子类会继承父类的所有属性和方法，并且可以添加自己特有的属性和方法。

```python
class ParentClass:
    def __init__(self, x):
        self.x = x

    def parent_method(self):
        print("This is a parent method.")

class ChildClass(ParentClass):
    def __init__(self, x, y):
        super().__init__(x)  # 调用父类的构造方法
        self.y = y

    def child_method(self):
        print("This is a child method.")

# 创建子类实例
child = ChildClass(1, 2)

# 调用继承的父类方法
child.parent_method()  # 输出: This is a parent method.

# 调用子类自己的方法
child.child_method()  # 输出: This is a child method.

# 访问继承的父类属性和子类自己的属性
print(child.x)  # 输出: 1
print(child.y)  # 输出: 2
```

## 12.4 类方法和静态方法

1. 类方法（class method）：
   - 类方法使用 `@classmethod` 装饰器进行标记，通常以 `cls` 作为第一个参数，表示类本身。
   - 可以通过类名或实例来调用类方法。
   - 类方法可以访问和修改类属性，并且可以在没有实例的情况下被调用。
   - 类方法常用于创建替代构造函数、操作共享数据等场景。

2. 静态方法（static method）：

   - 静态方法使用 `@staticmethod` 装饰器进行标记，不需要额外的参数来表示类或实例。
   - 可以通过类名或实例来调用静态方法。
   - 静态方法与类和实例无关，不能访问类属性或实例属性。
   - 静态方法通常用于封装逻辑上与类相关，但在执行过程中不需要类或实例的功能。

```python
class Car:
    total_cars = 0

    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
        Car.total_cars += 1

    @classmethod
    def from_string(cls, car_string):
        brand, model = car_string.split(',')
        return cls(brand, model)

    @staticmethod
    def is_brand_supported(brand):
        supported_brands = ['Toyota', 'Honda', 'Ford']
        return brand in supported_brands


# 使用类方法创建 Car 实例
car1 = Car.from_string('Toyota, Camry')  # 通过字符串创建实例
print(car1.brand)  # 输出：Toyota
print(car1.model)  # 输出：Camry
print(Car.total_cars)  # 输出：1

# 使用静态方法检查品牌是否受支持
print(Car.is_brand_supported('Toyota'))  # 输出：True
print(Car.is_brand_supported('BMW'))  # 输出：False

```

## 12.5 私有属性私有方法

1. 私有属性：

  - 使用两个下划线 `_` 开头的属性名来表示私有属性。

  - 私有属性只能在类的内部和类的方法中访问，无法在类的外部直接访问。

  - 可以通过公有方法来间接访问私有属性。

```python
class MyClass:
    def __init__(self):
        self._private_attr = 0  # 私有属性

    def public_method(self):
        self._private_attr += 1

# 在类的外部无法直接访问私有属性
obj = MyClass()
# print(obj._private_attr)  # 报错：AttributeError

# 通过公有方法间接访问私有属性
obj.public_method()
```

2.私有方法：

- 使用两个下划线 `_` 开头的方法名来表示私有方法。
- 私有方法只能在类的内部调用，无法在类的外部直接调用。
- 公有方法可以内部调用私有方法。

```python
class MyClass:
    def __private_method(self):
        print("This is a private method.")

    def public_method(self):
        # 在公有方法内部调用私有方法
        self.__private_method()

# 在类的外部无法直接调用私有方法
obj = MyClass()
# obj.__private_method()  # 报错：AttributeError

# 通过公有方法调用私有方法
obj.public_method()  # 输出："This is a private method."
```

## 12.6 多态

方法重写（Override）：

- 当子类继承父类时，可以重写父类的方法，以便在子类中提供对该方法的自定义实现。
- 在运行时，当调用该方法时，会根据对象的实际类型来确定使用哪个版本的方法。
- 子类可以完全覆盖父类的方法或在父类的基础上进行扩展。

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def make_sound(self):
        print("The animal makes a sound.")


class Dog(Animal):
    def __init(self,name):
        Animal.__init__(self, name)
        
    def make_sound(self):
        print("The dog barks.")


class Cat(Animal):
    def __init(self,name):
        Animal.__init__(self, name)
        
    def make_sound(self):
        print("The cat meows.")


# 多态使用
animals = [Dog("Buddy"), Cat("Whiskers")]
for animal in animals:
    animal.make_sound()

```

