
## 编译

### g++

### make

### cmake

## 关键字备忘

### C++11

typedef, struct, class, namespace, using, friend, inline, const, static, virtual, override, final, template, typename, auto, decltype, nullptr, this, new, delete, operator, sizeof, alignas, alignof, volatile, mutable, explicit, default, delete, noexcept, throw, try, catch, throw, static_assert, assert, __FILE__, __LINE__, __func__, __cplusplus, __STDC__, __STDC_VERSION__, __STDC_HOSTED__, __STDC_IEC_559__, __STDC_IEC_559_COMPLEX__, __STDC_ISO_10646__, __STDC_MB_MIGHT_NEQ_WC__, __STDCPP_STRICT_POINTER_SAFETY__, __STDCPP_THREADS__, __STDCPP_USE_NOEXCEPT, __STDCPP_USE_STATIC_ASSERT

typedef: 为类型取别名

```cpp
// samplpe1
typedef int integer;
integer a = 1;
// sample2
typedef int (*func)(int, int); // 定义了一个名为func的类型，这个类型是一个指向函数的指针，这个函数接受两个int类型的参数，并返回一个int类型的值。
// sample3
typedef struct Foo{
    int a;
    int b;
} Point; // 定义了一个名为Point的类型，这个类型是一个结构体，包含两个int类型的成员变量a和b。
```

关于sample2: [函数指针](https://www.runoob.com/w3cnote/cpp-func-pointer.html)

------------

typeof: 获取变量的类型, 返回变量的类型

```cpp
// sample1
int a = 1;
typeof(a) b = 2; 
```

decltype: 获取表达式的类型

```cpp
// sample1
int a = 1;
decltype(a) b = 2; 
```

nullptr: 空指针

sizeof: 获取变量的大小

