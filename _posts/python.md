> 主要用于记录一些高级使用技巧

参考: [廖雪峰Python教程](https://liaoxuefeng.com/books/python/)

## 异步IO

### 1. 协程(Couroutine)

协程是一种用户态的轻量级线程，**执行过程中，在子程序内部可中断，然后转而执行别的子程序，在适当的时候再返回来接着执行。**

协程的调度完全由用户控制。协程拥有自己的寄存器上下文和栈，协程调度切换时，将寄存器上下文和栈保存到其他地方，在切回来的时候，恢复先前保存的寄存器上下文和栈。因此协程能保留上一次调用时的状态，每次过程重入时，就相当于进入上一次调用的状态。

协程通过`async`和`await`关键字实现，`async`定义一个协程，`await`用于挂起执行。(Python3.5引入)

参考: [协程](https://liaoxuefeng.com/books/python/async-io/asyncio/index.html)
```python

import asyncio

async def hello(): # 定义一个协程
    print("Hello, world!")
    r = await asyncio.sleep(1) # `await`用于挂起协程
    print("Hello, again!")

if __name__ == "__main__":
    loop = asyncio.get_event_loop() # 获取一个事件循环
    loop.run_until_complete(hello())
    loop.close()
```

一个更复杂的例子:

```python
import asyncio

async def wget(host):
    print(f"wget {host}...")
    # 连接80端口:
    reader, writer = await asyncio.open_connection(host, 80)
    # 发送HTTP请求:
    header = f"GET / HTTP/1.0\r\nHost: {host}\r\n\r\n"
    writer.write(header.encode("utf-8"))
    await writer.drain()

    # 读取HTTP响应:
    while True:
        line = await reader.readline()
        if line == b"\r\n":
            break
        print("%s header > %s" % (host, line.decode("utf-8").rstrip()))
    # Ignore the body, close the socket
    writer.close()
    await writer.wait_closed()
    print(f"Done {host}.")

async def main():
    await asyncio.gather(wget("www.sina.com.cn"), wget("www.sohu.com"), wget("www.163.com"))

asyncio.run(main())
```

或者通过yield实现，yield可以返回一个值，也可以接收一个值。(Python2.5引入)

```python

def consumer():
    r = ""
    while True:
        n = yield r
        if not n:
            return
        print("[CONSUMER] Consuming %s..." % n)
        r = "200 OK"

def produce(c):
    c.send(None)
    n = 0
    while n < 5:
        n = n + 1
        print("[PRODUCER] Producing %s..." % n)
        r = c.send(n)
        print("[PRODUCER] Consumer return: %s" % r)
    c.close()

if __name__ == "__main__":
    c = consumer()
    produce(c)
```

## 高级特性/包

### 关于修饰器typing.overload

> 注意: 重载与多态的区别

由于python是动态类型语言，不支持函数重载，但是可以通过`typing.overload`实现函数重载。

```python
from typing import overload

class A:
    @overload
    def foo(self, x: int) -> int:
        pass

    @overload
    def foo(self, x: str) -> str:
        pass

    def foo(self, x):
        if isinstance(x, int):
            return x + 1
        elif isinstance(x, str):
            return x + "!"
        else:
            raise TypeError("x must be int or str")
```

### 关于修饰器classmethod和staticmethod

区别：

1. `@classmethod`修饰的方法，第一个参数是类对象，通常命名为`cls`，可以通过类对象调用，也可以通过实例对象调用。该方法**可以访问类属性，不能访问实例属性**。
   
  ```python
    class A:
        @classmethod
        def foo(cls):
            print(cls)
    A.foo() 
    # output: >>> <class '__main__.A'>
    # -------------------------
    # 常用于定义工厂方法:
    class B:
        def __init__(self, value):
            self.value = value
        @classmethod
        def create(cls, value):
            return cls(value)
    b = B.create(10)
    # -------------------------
  ```

2. `@staticmethod`修饰的方法，不需要传入类对象或实例对象，通常命名为`self`，可以通过类对象调用，也可以通过实例对象调用。该方法**不能访问类属性，也不能访问实例属性**。

  ```python
    class A:
        @staticmethod
        def foo():
            print("Hello, world!")
    A.foo()
    # output: >>> Hello, world!
  ```

### 包：weakref

> 关于深拷贝和浅拷贝：
> 深拷贝和浅拷贝的区别在于，浅拷贝只拷贝对象的引用，而深拷贝会拷贝对象的所有内容。
> 在Python赋值中，不明确区分深拷贝和浅拷贝，一般对静态数据类型(如int, str)进行赋值时，会进行深拷贝，对于动态数据类型(如list, dict)进行赋值时，会进行浅拷贝。

> 这个模块是我在翻torch源码时发现的，torch中的`torch.utils.hooks`模块中创建`hook`的`handle`对象时使用

`weakref`模块可以创建弱引用，弱引用不会增加对象的引用计数，当对象的引用计数为0时，对象会被销毁。

该模块可以用于解决循环引用问题，例如一个对象A引用了对象B，对象B又引用了对象A，这样两个对象的引用计数永远不会为0，导致内存泄漏。

```python
import weakref

class A:
    def __init__(self, value):
        self.value = value

    def __repr__(self):
        return str(self.value)

a = A(10)
d = weakref.WeakValueDictionary() # 创建一个弱引用字典
d["a"] = a # 将对象a加入字典
print(d["a"]) # 10
del a # 删除对象a
print(d["a"]) # None
```

## 杂记

str.encode()和bytes.decode()是互逆操作，str.encode()将字符串编码为字节，bytes.decode()将字节解码为字符串。

```python

s = "Hello, world!"
b = s.encode("utf-8")
print(b) # b'Hello, world!'
print(b.decode("utf-8")) # Hello, world!

```

python的复杂列表推导式:

```python

li = [i for i in range(5) for j in range(10) for k in range(20)]

# 等价于

li = []
for i in range(5):
    for j in range(10):
        for k in range(20):
            li.append(i)

```

