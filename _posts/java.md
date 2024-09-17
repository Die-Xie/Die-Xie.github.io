## 参考

[java常用库](https://www.cnblogs.com/zhaojinhui/p/18182739)

[java参考手册](https://www.apiref.com/java11-zh/index.html)

## 函数入口

程序入口main函数需要一个String[]参数，这个参数是命令行参数，可以通过命令行传入参数，也可以在IDE中配置参数。

```java
public class Foo{
    public static void main(String[] args){
        // codes
    }
}
```

## 关键字备忘

## 关于数组

### 数组

java中默认的数组是引用类型，数组的长度是**固定的**，一旦创建就不能改变。

```java
int a[] = new int[10]; // 创建一个长度为10的数组
```

### 动态数组

> java.util.ArrayList, 泛型，类似于C++的std::vector<>

```java
import java.util.ArrayList;

ArrayList<Integer> a = new ArrayList<Integer>();
a.add(1); // 添加元素
a.remove(0); // 删除第0个元素
a.size(); // 获取数组长度
a.get(0); // 获取第0个元素
a.set(0, 2); // 设置第0个元素为2
a.clear(); // 清空数组
a.isEmpty(); // 判断数组是否为空
a.contains(1); // 判断数组是否包含1
```
