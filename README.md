# notes4python
Some notes for python learning. Gleaned and sorted from [廖雪峰](https://www.liaoxuefeng.com/wiki/1016959663602400)

## 1 python基础
### 1.1 数据类型和变量
1. 转义符：\或r''
2. 分行：'''...'''
3. 布尔值
   - and：与运算
   - or：或运算
   - not：非运算
4. 空值：None
5. 浮点除：/，得精确值
6. 地板除：//，取结果整数部分
7. 取余：%，得到两个整数相除的余数

### 1.2 字符串和编码
1. ASCII/Unicode/UTF-8：
   - 为解决多语言编码冲突，Unicode统一了所有编码。为解决Unicode占用较多空间，可变长编码UTF-8诞生，将常用的英文字母被编码成1个字节，汉字通常是3个字节
   - 计算机内存中统一使用Unicode编码，当需要保存或传输时，就转换为UTF-8编码
   - 浏览网页时，服务器会把动态生成的Unicode内容转换为UTF-8再传输到浏览器
2. 字符串
   - ord()：获取字符的整数表示，ord('中')
   - chr()：将编码转换为对应的字符，chr(25991)
   - encode()：以Unicode表示的str通过编码为指定的bytes，'中文'.encode('utf-8')
   - decode()：从网络或磁盘上读取的字节流bytes转为str，b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
     - errors='ignore'：若bytes中包含无法解码的字节，使用ignore忽略错误， b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore')
   - len()：计算str包含多少个字符，len('中文')
3. 格式化
   - 占位符：%d：整数；%f：浮点数；%s：字符串；%x：十六进制整数

### 1.3 list和tuple
#### list
1. list：classmates = ['Michael', 'Bob', 'Tracy']
2. len()：获取列表元素个数/列表长度
3. []：获取list元素位置
   - classmates[0]，python默认索引从0开始
   - classmates[-1]，获取最后一个元素
4. 添加元素：
   - classmates.append('Adam')
   - classmates.insert(1, 'Jack')，添加jack到第二个位置
5. 删除元素：
   - classmates.pop()：删除末尾元素
   - classmates.pop(1)：删除指定位置元素
6. 赋值某个元素：
   - classmates[1] = 'Sarah'
7. 其他
   - list里元素数据类型可不同，L = ['Apple', 123, True]
   - list元素也可以是另一个list，s = ['python', ['asp', 'php']]
     - 取出'php'：s[1][1]

#### tuple
1. 与list区别：非常类似，但tuple一旦初始化就不能修改，更加安全
2. 定义方式：
   - t = (1, 2)，定义两个元素
   - t = ()，定义空集
   - t = (1, )，定义一个元素，不加逗号会和小括号歧义
   - 可变tuple：t = ('a', 'b', ['A', 'B'])

### 1.4 条件判断
1. if语句：
   - 示例：if <条件判断1>:  \n  elif <条件判断2>:  \n  <执行2>  \n  else:   \n  <执行4>
   - 注意：if语句执行从上往下判断，若在某个判断为True，则不再执行剩下的elif和else
   - 简写：if x:  \n  print('True')，只要x非零、非空，就为True

### 1.5 循环
1. for 循环
   - 格式：for x in ...
   - 生成数列：
     - a = list(range(5))  \n  print(a)
	 - for x in range(101)
2. while循环：只要条件满足，就不断循环
3. break语句：可以提前退出循环
    ```
    n = 1
    while n <= 100:
        if n > 10:
            break # 退出循环
        print(n)
        n = n + 1
    print('END')
    ```
4. continue：跳过当前的这次循环，直接开始下一次循环
    ```
    n = 0
    while n < 10:
        n = n + 1
        if n % 2 == 0:
            continue # 直接继续下一轮循环，不执行print()语句
        print(n)
    ```
5. pass语句:什么事也不做
   ```
    if age >= 18:
        pass
   ```
6. 不要滥用break和continue语句
   - break和continue会造成代码执行逻辑分叉过多，易出错

### 1.6 dict和set
#### dict
1. 定义：dict使用键-值（key-value）存储，具有极快的查找速度。
2. 原理：先在索引表里查该字对应的索引，然后直接翻到该页，找到这个字。
3. 定义方法：
   - d = {'Michael': 95, 'Bob': 75}，定义dict名为d
   - d['Adam'] = 67，添加Adam键，赋值为67，键不存在会报错
4. 判断键是否存在：
   - 'Thomas' in d：返回true或false
   - d.get('Thomas',1)：是则返回1
5. 删除字典元素：pop()
   - d.pop('Bob')

#### set
1. 和dict联系：
   - 和dict类似，是一组key的集合，但不存储value
   - 由于key不能重复，set中没有重复的key
2. 定义：s = set([1, 2, 3])
3. 性质：
   - 重复元素在set中自动被过滤
   - 无序
4. 添加元素：s.add(5)
5. 删除元素：s.remove(5)

## 2 函数
1. 定义函数
   ```
    def my_abs(x):
        if x >= 0:
            return x
        else:
            return -x
   ```
2. return：返回值
3. 默认参数：
   ```
   def power(x, n=2): # 2为n的默认参数
     s = 1
     while n > 0:
        n = n - 1
        s = s * x
     return s
   ```
   - 必选参数在前，默认参数在后。
4. 可变参数：可传入多个参数
   ```
   def calc(*numbers):
     sum = 0
     for n in numbers:
        sum = sum + n * n
     return sum
   ```
   - 批量传入可变参数：
    ```
        nums = [1, 2, 3]
        calc(*nums)
    ```
5. 递归函数
```
# 计算阶乘n! = 1 x 2 x 3 x ... x n
def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)
```

## 3 高级特性
### 3.1 切片
1. 取出数组中部分元素，list或tuple
   - L[0:3]：正取，从索引0开始取，直到索引3为止，但不包括索引3。
   - L[-2:-1]：倒取，从倒数第一个索引开始取，直到倒数第二个为止，但不包括倒数第二个。
   - L[::5]：间隔取，所有数，每5个取一个。
2. 字符串切片
   - 'abcd'也可以看成是list，每个元素就是一个字符：'abcd'[:2]
### 3.2 列表生成式
1. [x * x for x in range(1, 11) if x % 2 == 0] # [4, 16, 36, 64, 100]
2. [m + n for m in 'ABC' for n in 'XYZ'] # ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
3. [x if x % 2 == 0 else -x for x in range(1, 11)] # [-1, 2, -3, 4, -5, 6, -7, 8, -9, 10]，注意else位置
