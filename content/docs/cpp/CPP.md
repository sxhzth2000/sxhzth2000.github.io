---
title: C++
categories:
  - CPP
tags: []
date: 2024-06-14
---
C++知识

<!--more-->


# 面试问题
## 浅拷贝，深拷贝

深浅拷贝是面试经典问题，也是常见的一个坑 
- 浅拷贝：简单的赋值拷贝操作 
- 深拷贝：在堆区重新申请空间，进行拷贝操作
## const
对于非内部数据类型的输入参数，应该将“值传递”的方式改为“const 引用传递”，目的是提高效率。例如将void func(A a) 改为void func(const A &a)。  
对于内部数据类型的输入参数，不要将“值传递”的方式改为“const 引用传递”。否则既达不到提高效率的目的，又降低了函数的可理解性。例如void func(int x) 不应该改为void func(const int &x)。


（1）如果函数需要传入一个指针，是否需要为该指针加上const，把const加在指针不同的位置有什么区别；
- 如果你希望函数中的指针不能修改它所指向的值，使用 `const int *ptr`。
- 如果你希望函数中的指针不能修改它所指向的地址，使用 `int *const ptr`。
- 如果你希望函数中的指针既不能修改它所指向的值，也不能修改它所指向的地址，使用 `const int *const ptr`。
（2）如果写的函数需要传入的参数是一个复杂类型的实例，传入值参数或者引用参数有什么区别，什么时候需要为传入的引用参数加上const。
- **传值参数**：适用于小对象或不介意性能开销的场景。
- **传引用参数**：适用于需要修改传入对象且希望避免复制开销的场景。
- **传 `const` 引用参数**：适用于希望避免复制开销且保证函数内部不修改传入对象的场景。

## 范围for循环
这里的 `for (const auto& offset : offsets)` 是一种特定的 C++ 11 引入的语法，称为**范围 `for` 循环**（range-based for loop）。它简化了对容器或数组的遍历。让我们对比一下范围 `for` 循环和传统的 `for` 循环，并解释为什么在这种情况下使用范围 `for` 循环。

### 范围 `for` 循环

```cpp
std::array<Eigen::Vector2f, 4> offsets = {
    Eigen::Vector2f{0.25, 0.25},
    Eigen::Vector2f{0.75, 0.25},
    Eigen::Vector2f{0.25, 0.75},
    Eigen::Vector2f{0.75, 0.75}
};

for (const auto& offset : offsets) {
    if (insideTriangle(x + offset.x(), y + offset.y(), t.v)) {
        coverage += 0.25;
    }
}
```

### 传统 `for` 循环

如果使用传统的 `for` 循环，上述代码可以重写为：

```cpp
std::array<Eigen::Vector2f, 4> offsets = {
    Eigen::Vector2f{0.25, 0.25},
    Eigen::Vector2f{0.75, 0.25},
    Eigen::Vector2f{0.25, 0.75},
    Eigen::Vector2f{0.75, 0.75}
};

for (size_t i = 0; i < offsets.size(); ++i) {
    const auto& offset = offsets[i];
    if (insideTriangle(x + offset.x(), y + offset.y(), t.v)) {
        coverage += 0.25;
    }
}
```

### 范围 `for` 循环的优点


谭浩

1. **简洁性**：范围 `for` 循环使代码更简洁，更易读。它消除了管理循环索引变量的需要，并减少了潜在的错误（例如数组越界）。

2. **可读性**：通过范围 `for` 循环，可以直观地看出程序在遍历整个容器。这使得代码更易于理解和维护。

3. **安全性**：范围 `for` 循环避免了循环变量超出数组边界的风险，因为它自动遍历整个容器。

4. **效率**：范围 `for` 循环在某些情况下可以更高效，因为编译器可以对其进行优化。

### 什么时候使用范围 `for` 循环

范围 `for` 循环非常适合遍历整个容器（例如数组、`std::vector` 等），特别是当不需要使用循环索引时。它可以提高代码的可读性和维护性，使代码更简洁。

在你的例子中：

```cpp
for (const auto& offset : offsets) {
    if (insideTriangle(x + offset.x(), y + offset.y(), t.v)) {
        coverage += 0.25;
    }
}
```

使用范围 `for` 循环遍历 `offsets` 数组是非常合适的，因为我们只需要访问每个元素，而不需要使用索引。这种方式使代码更简洁和清晰。

## const 与函数

# externC C++中c的代码片段
是的，如果其他C文件（以 `.c` 扩展名保存）使用了你提到的代码片段，它将以C的形式编译。这个代码片段的设计目的是为了使得C和C++编译器都能正确处理代码，具体来说：

### 代码片段解析

```cpp
#include <stdio.h>

// 如果是C++编译器，定义一个宏
#ifdef __cplusplus
extern "C" {
#endif

// 这里是C和C++都能编译的代码
struct Point {
    int x;
    int y;
};

// 函数声明
void modifyPoint(struct Point *p);

#ifdef __cplusplus
}
#endif
```

### 解释

1. **`extern "C"`**：
   - 在C++编译环境中，`extern "C"` 告诉编译器使用C语言链接规范来处理被包含在 `extern "C"` 块中的函数或变量声明。
   - 在C语言编译环境中，`extern "C"` 语法会被忽略，因此不会影响C语言编译过程。

2. **条件编译**：
   - `#ifdef __cplusplus` 和 `#endif` 用于判断是否在C++编译环境中。如果是C++编译器，则会定义 `extern "C"`，否则不做任何处理。
   - 在C编译环境中，`__cplusplus` 宏未定义，因此 `extern "C"` 部分不会出现，代码将以C语言编译。

### 文件示例

假设有两个文件，一个是C语言源文件 `file1.c`，另一个是C++语言源文件 `file2.cpp`，它们都需要使用相同的头文件 `common.h`。

**`common.h`**:

```cpp
#ifndef COMMON_H
#define COMMON_H

#include <stdio.h>

#ifdef __cplusplus
extern "C" {
#endif

struct Point {
    int x;
    int y;
};

void modifyPoint(struct Point *p);

#ifdef __cplusplus
}
#endif

#endif // COMMON_H
```

**`file1.c`**:

```c
#include "common.h"

void modifyPoint(struct Point *p) {
    p->x = 10;
    p->y = 20;
}

int main() {
    struct Point pt = {0, 0};
    modifyPoint(&pt);
    printf("pt.x = %d, pt.y = %d\n", pt.x, pt.y);
    return 0;
}
```

**`file2.cpp`**:

```cpp
#include "common.h"
#include <iostream>

void printPoint(const Point &p) {
    std::cout << "Point(" << p.x << ", " << p.y << ")" << std::endl;
}

int main() {
    Point pt = {0, 0};
    modifyPoint(&pt);
    printPoint(pt);
    return 0;
}
```

### 编译

- **编译C文件**：当 `file1.c` 被C编译器（如 `gcc`）编译时，编译器将处理 `common.h` 文件中的 `extern "C"` 语法，并按照C语言规范处理 `modifyPoint` 函数声明和实现。
  
- **编译C++文件**：当 `file2.cpp` 被C++编译器（如 `g++`）编译时，编译器将处理 `common.h` 文件中的 `extern "C"` 语法，确保 `modifyPoint` 函数使用C链接规范，以便于链接C语言和C++代码。

### 总结

- **C文件**（`.c`）编译器会忽略 `extern "C"` 语法，只按照C语言规范编译代码。
- **C++文件**（`.cpp`）编译器会处理 `extern "C"` 语法，确保C语言函数可以被C++代码正确链接。
- 使用 `extern "C"` 和条件编译，可以使头文件同时兼容C和C++编译环境，支持跨语言的代码共享。