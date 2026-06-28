# 【半小时入门Python】从零开始速成Python上机考试

> 原创 已于 2026-04-05 18:20:42 修改 · 公开 · 387 阅读 · 11 · 7 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/159251810

**目录**

[TOC]





## 注意项

> 
> 
> - 在 Python 中， **空的容器（空列表、空字符串、空字典）在 `if` 语句中等价于 `False`** 。
> 
> - 只要是 **可迭代** 的，都能 **解包赋值** ，但要注意 **数量必须匹配** 。
> 
> 

## 常用库函数

###  **数学计算** 

```python
sum([1,2,3])        # 6 求和
max([1,2,3])        # 3 最大值
min([1,2,3])        # 1 最小值
abs(-5)             # 5 绝对值
pow(2, 10)          # 1024 次方
round(3.14159, 2)   # 3.14 四舍五入
```

###  **常用math库** 

```lua
import math
math.sqrt(9)        # 3.0 开平方
math.ceil(3.2)      # 4 向上取整
math.floor(3.8)     # 3 向下取整
math.pi             # 3.14159...
math.inf            # 无穷大
```

---

### 随机数

```python
import random
 
# 生成0到10之间的随机整数（包括0和10）
print(random.randint(0, 10))
# 生成1到10之间（不包括10）的随机整数
print(random.randrange(1, 10))
# 生成0到1之间的随机浮点数（不包括1）
print(random.random())
# 生成1到3之间的随机浮点数
print(random.uniform(1, 3))
 
# 特定序列随机选择元素
list1 = [1, 2, 3, 4, 5]
random_element = random.choice(list1)
# 从列表中随机选择3个不重复的元素
print(random.sample(list1 , 3))
# 序列随机排序
list1 = [1, 2, 3, 4, 5]
random.shuffle(list1)
 
# 正态分布
print(random.normalvariate(0, 1))
```

###  ***列表操作** 

```python
a = [3,1,2]
len(a)              # 3 长度
sorted(a)           # [1,2,3] 排序（不改变原列表）
sorted(a, reverse=True)  # [3,2,1] 倒序
a.sort()            # 直接改变原列表
 
s.reverse()         # 倒置
a.append(4)         # 末尾添加
 
a.pop()             # 删除末尾
a.pop(2)            # 弹出下标2 → 1
a.count(3)          # 统计3出现次数
a.index(3)          # 3第一次出现的下标
 
del my_list[1]      # 删除索引 1 的元素
a.remove("a")            # 根据元素值进行删除
 
sum(a)              # 求和
 
a[-1]# 看最后一个。
a[0]# 看第一个。
```

---

###  ***字符串操作** 

```python
s = "Hello123"
 
# 判断类型
s.isalnum()     # True  全是字母或数字
s.isalpha()     # False 全是字母
s.isdigit()     # False 全是数字
s.islower()     # False 全是小写
s.isupper()     # False 全是大写
s.isspace()     # False 全是空白
 
# 大小写转换
s.lower()       # "hello123"
s.upper()       # "HELLO123"
 
# 查找
s.count("l")    # 2
s.find("l")     # 2  找不到返回-1
s.index("l")    # 2  找不到报错
 
# 替换
str.replace(old, new[, max])
# 可选字符串, 替换不超过 max 次
 
ord("a")        # 97   字符转ASCII码
chr(97)         # "a"  ASCII码转字符
```

#### split

> 注：返回 **列表** 

```python
# 智能分割：把所有的连续空白符（换行 \n、空格、制表符 \t）都当成切分符，并且会自动忽略掉开头和结尾的空元素。
s.split()           
s.split()        # ["1", "2", "3"]  默认按空格切
s.split(' ')     # ["1", "2", "3"]  指定空格切
s.split('\n')    # ["1 2 3"]        按换行符切
```

#### strip

> 注：返回 **字符串** 

```python
s.strip()    # 去首尾空白
s.strip()    # "hello"   两端都去
s.lstrip()   # "hello  " 只去左边
s.rstrip()   # "  hello" 只去右边
"***hello***".strip('*')   # "hello"
"123hello123".strip('123') # "hello"
```

### 集合操作

```python
set1 = {1, 2, 3, 4}            # 直接使用大括号创建集合
set2 = set([4, 5, 6, 7])      # 使用 set() 函数从列表创建集合
# 创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典
 
s.add(4)        # 添加元素 → {1,2,3,4}
s.remove(1)     # 删除元素，找不到报错
s.discard(1)    # 删除元素，找不到不报错
len(s)          # 元素个数
3 in s          # True  判断是否存在
3 not in s      # False
 
a | b    # {1,2,3,4}  并集
a & b    # {2,3}      交集
a - b    # {1}        差集（a有b没有）
a ^ b    # {1,4}      对称差集（只在一个里面的）
 
s[0]        # ❌ 报错！集合没有下标
list(s)[0]  # ✅ 转成列表再取
```

### 元组操作

```python
# 创建
t = (1, 2, 3)
t = (1,)        # 单元素元组，必须加逗号
t = 1, 2, 3     # 省略括号也可以
t = tuple([1,2,3])  # 列表转元组
 
# 取值
t = (1, 2, 3, 4, 5)
t[0]      # 1
t[-1]     # 5
t[1:3]    # (2, 3)
t[::-1]   # (5,4,3,2,1)
 
 
t = (1, 2, 2, 3)
len(t)        # 4
t.count(2)    # 2  统计出现次数
t.index(2)    # 1  第一次出现的下标
2 in t        # True
max(t)        # 3
min(t)        # 1
sum(t)        # 8
```

### 字典操作

```python
# 字典可以判相等 顺序不影响，键值对一样就相等
d = {"a": 1, "b": 2, "c": 3}
d = {}              # 空字典
d = dict()          # 空字典
 
d["a"]              # 1
d.get("a")          # 1
d.get("a"，0)       # 找不到不报错
 
d["b"] = 2          # 添加/修改
del d["a"]          # 删除，找不到报错
d.pop("a")          # 删除并返回值，找不到报错
d.pop("a", 0)       # 找不到返回0，不报错
d.clear()           # 清空
 
for key in d:               # 遍历key
    print(key)              # a b
 
for key, val in d.items():  # 遍历key和value
    print(key, val)         # a 1 / b 2
 
for val in d.values():      # 只遍历value
    print(val)              # 1 2
 
for key in d.keys():        # 只遍历key
    print(key)              # a b
 
 
len(d)              # 2     元素个数
"a" in d            # True  判断key是否存在
d.keys()            # 所有key
d.values()          # 所有value
d.items()           # 所有键值对
```

---

###  **类型转换** 

#### 普通转换

```scss
int("123")          # 123
float("3.14")       # 3.14
str(123)            # "123"
list("abc")         # ["a","b","c"]
list((1,2,3))       # [1,2,3]
```

### join详解

```python
"分隔符".join(元素)
#列表、字符串、元组、字典
 
a = ["a", "b", "c"]
"".join(a)     # "abc"    无缝拼接
" ".join(a)    # "a b c"  空格分隔
",".join(a)    # "a,b,c"  逗号分隔
"-".join(a)    # "a-b-c"  横线分隔
 
a = [1, 2, 3]
" ".join(a)              # ❌ 报错！元素是数字
" ".join(map(str, a))    # ✅ "1 2 3"
 
 
#join与split互逆
# split：字符串 → 列表
"a b c".split()          # ["a", "b", "c"]
# join：列表 → 字符串
" ".join(["a","b","c"])  # "a b c"
```

### sort详解

```python
# !!!.sort()返回None
list.sort(cmp=None, key=None, reverse=False)
# cmp -- 可选参数, 如果指定了该参数会使用该参数的方法进行排序。
# key -- 用来进行比较的元素，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
# reverse -- 排序规则，reverse = True 降序， reverse = False 升序（默认）。
 
my_list.sort(key=len)
sorted_list = sorted(my_list, key=lambda x: x[-1])
```

### map详解

```python
map(function, iterable, ...)
# function：要作用于可迭代对象（如列表、元组等）每个元素的函数。
# iterable：一个或多个可迭代对象。
## 返回一个map对象，必须通过转化为list或其他可迭代类型来查看结果。
 
# 字符串列表转整数
map(int, ["1","2","3"])      # 1 2 3
list(map(int, ["1","2","3"])) # [1, 2, 3]
 
# 整数列表转字符串
map(str, [1, 2, 3])          # "1" "2" "3"
list(map(str, [1, 2, 3]))    # ["1", "2", "3"]
 
# 转浮点数
list(map(float, ["1.1","2.2"])) # [1.1, 2.2]
```

### filter详解

```python
filter(function, iterable)
# function：用于筛选元素的函数，该函数应返回一个布尔值，表示元素是否符合筛选条件。
# iterable：待筛选的序列，可以是列表、元组、集合等可迭代对象。
# 返回值filter函数返回一个由符合条件的元素组成的新列表。
 
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]  
even_numbers = filter(lambda x: x % 2 == 0, numbers)  
print(list(even_numbers))  # Output: [2, 4, 6, 8]
```

### 切片

#### 切片基础

> 切片可以用在字符串，列表及元组上。

```python
# 格式：[start : end : step]
 
a = [0, 1, 2, 3, 4, 5]
s = "012345"
 
a[1:3]    # [1, 2]        从1取到2，取不到3
a[:3]     # [0, 1, 2]     从头取到2
a[2:]     # [2, 3, 4, 5]  从2取到末尾
a[:]      # 全部
a[-1]     # 5             最后一个
a[-2:]    # [4, 5]        最后两个
a[:-2]    # [0,1,2,3]     除了最后两个
 
# 带步长
a[::2]    # [0, 2, 4]     每隔一个
a[::3]    # [0, 3]        每隔两个
a[::-1]   # [5,4,3,2,1,0] 倒序
a[4:1:-1] # [4, 3, 2]     从4倒着取到2
 
# 负数
a[-1]   # 最后一个
a[-2]   # 倒数第二个
a[-3:]  # 最后三个
```

#### 切片赋值

```python
# 把切片放在赋值语句的左边，或把它作为del操作的对象
# 就可以对序列进行嫁接、切除或就地修改操作。
a[:] = [4, 5, 6]   # 直接修改原列表内容
```

### *引用与复制

```cobol
# 引用（同一个对象）
b = a
 
# 复制
b = a[:]           # 浅复制
b = a.copy()       # 浅复制
b = list(a)        # 浅复制
import copy
b = copy.deepcopy(a)  # 深复制
 
# 浅拷贝与深拷贝
# 一维列表 → 浅拷贝就够了
a = [1, 2, 3]
b = a[:]
 
# 二维列表 → 用深拷贝或列表推导式
import copy
b = copy.deepcopy(a)
 
# 或者列表推导式（更常用）
b = [row[:] for row in a]
```

---

### f-string详解

```python
# 变量
name = "小明"
age = 18
print(f"我叫{name}，今年{age}岁")   # "我叫小明，今年18岁"
 
# 数字
x = 3.14159
 
f"{x:.2f}"    # "3.14"    保留2位小数
f"{x:.0f}"    # "3"       保留0位小数
f"{x:10.2f}"  # "      3.14"  总宽度10，右对齐
f"{x:<10.2f}" # "3.14      "  总宽度10，左对齐
f"{x:010.2f}" # "0000003.14"  总宽度10，用0补齐
 
# 整数
n = 42
f"{n:5d}"     # "   42"   总宽度5，右对齐
f"{n:<5d}"    # "42   "   总宽度5，左对齐
f"{n:05d}"    # "00042"   总宽度5，用0补齐
 
# 字符串
s = "hi"
f"{s:10s}"    # "hi        "  总宽度10，左对齐
f"{s:>10s}"   # "        hi"  总宽度10，右对齐
f"{s:^10s}"   # "    hi    "  总宽度10，居中
```

---

###  **collections库（竞赛常用）** 

```python
from collections import Counter, defaultdict, deque
 
# Counter 统计频率
c = Counter([1,1,2,3])       # 返回一个字典{1:2, 2:1, 3:1}
c.most_common(2)             # [(3, 3), (2, 2)] # 出现最多的N个
 
# defaultdict 带默认值的字典
d = defaultdict(int)     # 默认值为0，不会报KeyError
d["a"] += 1
 
# deque 双端队列
q = deque([1,2,3])
q.appendleft(0)          # 左边添加
q.popleft()              # 左边删除
d.count('a')             # 计算 deque 中元素等于 x 的个数。
a.extend(b)              # 在a队列右侧，添加另一个iterable参数b中的元素。
d.index('w')             # 返回索引，找不到则报错
a.insert(1,'X')          # 插入
a.remove('a')            # 移除找到的第一个值。
 
# 向右循环移动
d = deque('ghijkl')
d.rotate(1)              # -1是往左循环移动
# deque(['l', 'g', 'h', 'i', 'j', 'k'])
```

### itertools库（竞赛常用）

```python
# 全排列
from itertools import permutations
ls = []
for item in permutations(nums):
    ls.append(item)
return ls
 
# 组合，取2个
print(list(combinations(l, 2)))
# [(1,2), (1,3), (2,3)]
 
# 前缀和
from itertools import accumulate
s = list(accumulate(a))
print(s)  # [1, 3, 6, 10, 15]
```

---

###  **enumerate 和 zip** 

```python
# enumerate 带下标遍历
for i, x in enumerate([10,20,30]):
    print(i, x)    # 0 10 / 1 20 / 2 30
 
# zip按位置解包 同时遍历两个列表
a = [1,2,3]
b = [4,5,6]
for x, y in zip(a, b):
    print(x, y)    # 1 4 / 2 5 / 3 6
```

### 离线查询

```python
# 查询某函数用法
help(sorted)
# 查询某类型下的方法
help(int)
# 列出某类型的所有方法
dir(float)
 
 
```

## 常用语法

### 列表推导式

```python
# 先生成整个列表再求和
[表达式 for 变量 in 可迭代对象 <if 条件>]
[表达式 <if 条件 else 表达式> for 变量 in 可迭代对象 ]
 
result = [x for x in a if x != 0]
nums = [x if x % 2 == 0 else 0 for x in range(10)]
```

### 生成器表达式

```python
colors = ['Black', 'White', 'Yellow']
sizes = ['XS', 'S', 'M', 'L', 'XL']
t_shirt_models = ((color, size) for color in colors for size in sizes)
# 嵌套循环
print(t_shirt_models)
# Output:<generator object <genexpr> at 0x0000020CE2EC4C48>
#由于输出迭代器，因此生成器表达式后一般跟类型转换
 
# 取数据
for t in t_shirt_models:
    print(t)
```

### 匿名函数

```python
lambda arguments: expression
# arguments 是参数列表，可以包含零个或多个参数，但必须在冒号(:)前指定。
# expression 是一个表达式，用于计算并返回函数的结果。
 
x = lambda a : a + 10
print(x(5))
# 15
```

## 模板

### ACM模式IO

#### 按行取输入

```python
import sys
 
for line in sys.stdin:
    if not line.strip():
        continue
    tyr:
        nums = list(map(int, line.split()))
        
        a = nums[0]
        b = nums[1]
        res = a + b
        print(res)
    
    except:
        break
```

#### 整体取输入

```python
import sys
 
data = sys.stdin.read().splitlines()
idx = 0
 
# 分组取
# for _ in range(t):
    # 然后按需要一行一行取：
    line1 = data[idx]; idx += 1 
    #  如果输入的是列表
    line1 = eval(data[idx]): idx += 1
```

### 一维列表传参输入

智能分割（所有空白格）：

```python
data = sys.stdin.read().split()
res = process(list(map(int, data)))
```

按行分割：

```python
# 或者这里可以直接用splitlines()，后续就不用条件过滤
data = sys.stdin.read().split('\n')
res = process([int(line) for line in data if line.strip()])
```

### 二维列表传参输入

> **注：split('\n')切割后最后会多出空行，因此必须使用line.strip()过滤** 

```python
data = sys.stdin.read().split('\n')
res = process([list(map(int, line.split())) for line in data if line.strip()])
```

### 输出

```python
# 加分隔符输出
print(a, b, sep = "\n")
 
# 三引号多行输出
print("""aaa
         bbb
         ccc""")
 
# 列表输出转换
print(" ".join(map(str, sorted(nums))))  # 数字列表先转换为字符列表后再空格拼接
```

### 常用技法

#### 字符串清洗：只保留字母

```python
# 字符清洗：只保留字母
        string = ""
        for char in data:
            if 'a' <= char <= 'z' or 'A' <= char <= 'Z':
                char = char.lower()
                string += char
```

#### 快速初始化二维数组

```python
ls = [[0] * m for _ in range(n)]
```

#### 快速初始化整数序列

```python
# 1到n
l = list(range(1, n+1))   # [1, 2, 3, 4, 5]
# 带步长
l = list(range(0, 20, 2)) # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

#### 多维数组内部序列去重（三数之和）

```python
res = set()
for item in permutations(nums, 3):
    res.add(tuple(sorted(item))) # 集合元素必须可哈希，因此要先转换为元组
```

#### 二维数组按端点排序

```python
# 使用匿名函数按每个子序列第一个元素大小排列
ls.sort(key=lambda x: x[0])
```

#### 环形下标

```python
n = 5
# 环形遍历：从某位置往后走k步
idx = (idx + k) % n
# 约瑟夫环：数m个人
idx = (idx + m - 1) % len(people)
# 循环数组：下一个位置
next_idx = (i + 1) % n
# 循环数组：上一个位置
prev_idx = (i - 1 + n) % n
# 星期几：今天是day，k天后是
day = (day + k) % 7
```

#### 去重

##### 列表去重

```python
a = [1,2,2,3,3,4]
 
# 方法1：set（最简单）
list(set(a))           # [1,2,3,4] 顺序不保证
 
# 方法2：保留顺序去重
list(dict.fromkeys(a)) # [1,2,3,4] 保留原顺序
 
# 方法3：列表推导式
res = []
[res.append(x) for x in a if x not in res]  # [1,2,3,4]
```

##### 二维列表去重

```python
a = [[1,2],[1,2],[3,4]]
 
# 转tuple加入集合
res = set(tuple(x) for x in a)
[list(x) for x in res]    # [[1,2],[3,4]]
 
# 或者
list(map(list, set(map(tuple, a))))
```

##### 遍历时跳过重复

```python
nums = [1,1,2,2,3]
nums.sort()
 
for i in range(len(nums)):
    if i > 0 and nums[i] == nums[i-1]:
        continue    # 跳过重复
    print(nums[i])  # 1 2 3
```

##### 字符串去重

```python
s = "aabbcc"
 
# 去重保留顺序
"".join(dict.fromkeys(s))   # "abc"
 
# 去重不保留顺序
"".join(set(s))             # 顺序不保证
```

##### Counter去重统计

```python
from collections import Counter
a = [1,1,2,2,3]
Counter(a).keys()    # dict_keys([1,2,3])  去重
list(Counter(a))     # [1,2,3]
```

#### *字符串倒置

```python
s = 'abcde'
s[::-1]  # 直接倒置
"".join(reversed(s))  # 空字符连接倒置
```

#### **字符串列表双重倒置

```python
data[idx] = 'abc def'
str = [s[::-1] for s in data[idx].split()][::-1]
```

### 字符串特定位置插入

```python
s = "hello"
# 在下标2的位置插入"XYZ"
s = s[:2] + "XYZ" + s[2:]
# "he" + "XYZ" + "llo" = "heXYZllo"
```

#### 二分查找

##### bisect详解

```python
from bisect import bisect_left, bisect_right, insort
 
bisect_left(a, x)    # x位置（有重复值时左边）
bisect_right(a, x)   # x位置（有重复值时右边）
insort(a, x)         # 插入x并保持有序
 
# 插入元素4
bisect.insort_left(sorted_list, 4)
```

##### 二分查找模板

```python
# 二分查找模板
from bisect import bisect_left
 
# 在有序数组中找 x
a.sort()
pos = bisect_left(a, x)
if pos < len(a) and a[pos] == x:
    print(f"Found at index {pos}")
```

### 转置矩阵

```python
# n行m列 --> m行n列
n, m = map(int, data[idx].split()); idx += 1
mat = []
for _ in range(n):
    mat.append(list(map(int, data[idx].split()))); idx += 1
 
# 转置
mat_c = [[mat[j][i] for j in range(n)] for i in range(m)]
```

```python
# zip按位置解包
mat_c = [list(row) for row in zip(*mat)]
```

### 链表

```python
import sys
 
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
 
# 把 {1,2,3} 转成链表
def build(s):
    s = s[1:-1]
    if not s: return None
    vals = s.split(',')
    head = ListNode(int(vals[0]))
    cur = head
    for v in vals[1:]:
        cur.next = ListNode(int(v))
        cur = cur.next
    return head
 
# 反转
def reverse(head):
    p, c = None, head
    while c:
        c.next, p, c = p, c, c.next
    return p
 
# 输出
def print_list(head):
    res = []
    while head:
        res.append(str(head.val))
        head = head.next
    print("{" + ",".join(res) + "}")
 
# ===== 你的输入方式 =====
data = sys.stdin.read().splitlines()
idx = 0
 
head = build(data[idx]); idx += 1
new_head = reverse(head)
print_list(new_head)
```

### 二叉树

#### 种树

```python
import sys
 
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
 
# 把 {1,2,3,#,#,4,5} 转成二叉树（层序构建）
def build(s):
    s = s[1:-1]
    if not s: return None
    vals = s.split(',')
    root = TreeNode(int(vals[0]))
    queue = [root]
    idx = 1
    while queue and idx < len(vals):
        node = queue.pop(0)
        # 左孩子
        if idx < len(vals) and vals[idx] != '#':
            node.left = TreeNode(int(vals[idx]))
            queue.append(node.left)
        idx += 1
        # 右孩子
        if idx < len(vals) and vals[idx] != '#':
            node.right = TreeNode(int(vals[idx]))
            queue.append(node.right)
        idx += 1
    return root
 
# ===== 你的输入方式 =====
data = sys.stdin.read().splitlines()
idx = 0
 
root = build(data[idx]); idx += 1
```

#### 遍历

```python
# ===== 四种遍历 =====
 
# 前序：根→左→右
def preorder(root):
    if not root: return []
    return [root.val] + preorder(root.left) + preorder(root.right)
 
# 中序：左→根→右
def inorder(root):
    if not root: return []
    return inorder(root.left) + [root.val] + inorder(root.right)
 
# 后序：左→右→根
def postorder(root):
    if not root: return []
    return postorder(root.left) + postorder(root.right) + [root.val]
 
# 层序：一层一层从左到右
def levelorder(root):
    if not root: return []
    res = []
    queue = [root]
    while queue:
        node = queue.pop(0)
        res.append(node.val)
        if node.left: queue.append(node.left)
        if node.right: queue.append(node.right)
    return res
```

### 常见错误与优化技巧

#### 错误

> 
> 
> - 部分用例：
> 
>   - 超时
> 
>   - 循环中变量未重置
> 
>   - 全局变量初始化问题（如含负数，但仍初始化为0）
> 
> - strip()返回字符串，后[0]取出的是单个字符；split()返回字符列表，后[]取的是字符串
> 
> - 复制与引用
> 
>   - list赋值是引用，修改会互相影响
> 
>   - append列表要副本，用[:]复制一份
> 
>   - 二维初始化用推导式，不用*号
> 
>   - 回溯结果存path[:]，不存path
> 
>   - 函数内改列表用[:]赋值，不用=
> 
> - 无输出结果
> 
>   - 检查输出类型是否正确
> 
>     - "".join()只接受字符型可迭代对象
> 
> 

#### 优化

##### *查找优化

```python
# ❌ 列表查找 O(n)
if x in list
 
# ✅ 集合/字典查找 O(1)
if x in set
if x in dict
```

##### 排序+二分 替代 线性查找

数组查找下标

```python
# ❌ 线性查找 O(n)
nums.index(x)
 
# ✅ 排序后二分 O(log n)
from bisect import bisect_left
pos = bisect_left(nums, x)
```

##### 哈希表 替代 双重循环

两数之和、A-B=C数对

```python
# ❌ 暴力双循环 O(n²)
for i in range(n):
    for j in range(i+1, n):
 
# ✅ 哈希表 O(n)
seen = {}
for i, val in enumerate(nums):
    if target - val in seen:
        return [seen[target-val], i]
    seen[val] = i
```

##### 前缀和 替代 重复求和

```python
# ❌ 每次重新求和 O(n)
sum(nums[i:j])
 
# ✅ 前缀和 O(1)查询
prefix = [0] * (n+1)
for i in range(n):
    prefix[i+1] = prefix[i] + nums[i]
# 区间[i,j]的和 = prefix[j+1] - prefix[i]
```

##### 双端队列 替代 暴力窗口

```python
# ❌ 每次取max O(k)，总体O(nk)
max(nums[i:i+k])
 
# ✅ 双端队列 O(n)
from collections import deque
dq = deque()   # 存下标，保持递减
```

##### 双指针 替代 双重循环

```python
# ❌ 暴力 O(n²)
for i in range(n):
    for j in range(i+1, n):
 
# ✅ 双指针 O(n)
left, right = 0, len(nums)-1
while left < right:
    if 满足条件:
        left += 1
        right -= 1
```

##### 迭代 替代 递归

```python
# ❌ 递归 n>1000崩溃
def fib(n):
    return fib(n-1) + fib(n-2)
 
# ✅ 迭代
a, b = 0, 1
for _ in range(n):
    a, b = b, a+b
```

##### 滑动窗口 替代 暴力子串

```python
# ❌ 暴力 O(n²)
for i in range(n):
    for j in range(i, n):
 
# ✅ 滑动窗口 O(n)
left = 0
for right in range(len(s)):
    while 不满足条件:
        left += 1
```

##### Counter 替代 手动统计

```python
# ❌ 手动统计
d = {}
for c in s:
    d[c] = d.get(c, 0) + 1
 
# ✅ Counter一行搞定
from collections import Counter
Counter(s)
```