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

## 杂记

str.encode()和bytes.decode()是互逆操作，str.encode()将字符串编码为字节，bytes.decode()将字节解码为字符串。

```python

s = "Hello, world!"
b = s.encode("utf-8")
print(b) # b'Hello, world!'
print(b.decode("utf-8")) # Hello, world!

```

