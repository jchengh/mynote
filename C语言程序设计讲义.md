# C语言程序设计讲义

---

## 目录

1. [C语言简介](#第一章-c语言简介)
2. [开发环境](#第二章-开发环境)
3. [基本语法](#第三章-基本语法)
4. [数据类型](#第四章-数据类型)
5. [变量与常量](#第五章-变量与常量)
6. [运算符与表达式](#第六章-运算符与表达式)
7. [程序结构](#第七章-程序结构)
8. [选择结构](#第八章-选择结构)
9. [循环结构](#第九章-循环结构)
10. [数组](#第十章-数组)
11. [函数](#第十一章-函数)
12. [指针](#第十二章-指针)
13. [字符串](#第十三章-字符串)
14. [结构体](#第十四章-结构体)
15. [文件操作](#第十五章-文件操作)
16. [预处理](#第十六章-预处理)
17. [动态内存管理](#第十七章-动态内存管理)
18. [常见错误与调试](#第十八章-常见错误与调试)
19. [标准库函数](#附录a-标准库函数速查)
20. [ASCII码表](#附录b-ascii码表)

---

## 第一章 C语言简介

### 1.1 C语言的历史

C语言是一种通用的、面向过程式的计算机程序设计语言。1972年，为了移植与开发UNIX操作系统，丹尼斯·里奇（Dennis Ritchie）在贝尔电话实验室设计开发了C语言。

**C语言发展历程：**

| 时间 | 标准 | 说明 |
|------|------|------|
| 1972 | - | C语言诞生 |
| 1978 | K&R C | Brian Kernighan和Dennis Ritchie出版《The C Programming Language》 |
| 1989 | ANSI C (C89) | 美国国家标准协会标准化 |
| 1990 | ISO C (C90) | 国际标准化组织采纳ANSI C |
| 1999 | C99 | 添加了inline、bool、long long等特性 |
| 2011 | C11 | 添加了多线程、Unicode支持等 |
| 2018 | C17/C18 | 主要是bug修复 |

### 1.2 C语言的特点

| 特点 | 说明 |
|------|------|
| 高效性 | C语言程序执行效率高，接近汇编语言 |
| 可移植性 | 只需少量修改即可在不同平台运行 |
| 灵活性 | 语法简单，表达能力强 |
| 丰富的运算符 | 支持多种运算符进行各种运算 |
| 结构化控制 | 支持if-else、switch、while、for等控制结构 |
| 丰富的库函数 | 提供大量标准库函数 |
| 中级语言 | 既能进行高级操作，也能进行低级操作 |

### 1.3 C语言的应用领域

```
┌─────────────────────────────────────────────────────────────┐
│                        C语言应用领域                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │
│  │  操作系统   │  │  嵌入式系统 │  │  驱动程序   │        │
│  └─────────────┘  └─────────────┘  └─────────────┘        │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │
│  │  编译器开发  │  │  数据库系统  │  │  游戏开发   │        │
│  └─────────────┘  └─────────────┘  └─────────────┘        │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │
│  │  网络协议   │  │  图像处理   │  │  科学计算   │        │
│  └─────────────┘  └─────────────┘  └─────────────┘        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 1.4 第一个C程序

```c
/* 我的第一个C程序 */
#include <stdio.h>

int main() {
    /* 在屏幕上输出 Hello, World! */
    printf("Hello, World!\n");
    
    /* 返回0表示程序正常结束 */
    return 0;
}
```

**程序解析：**

| 代码部分 | 说明 |
|----------|------|
| `/* ... */` | 多行注释，用于说明程序 |
| `#include <stdio.h>` | 预处理指令，引入标准输入输出头文件 |
| `int main()` | 主函数，程序入口，每个C程序必须有且只有一个main函数 |
| `{ }` | 函数体开始和结束的标志 |
| `printf("Hello, World!\n");` | 调用printf函数输出字符串，\n表示换行 |
| `return 0;` | 返回0表示程序正常结束 |

### 1.5 C程序执行流程

```
┌────────────────────────────────────────────────────────────────┐
│                      C程序编译执行流程                            │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  源代码.c  ──┬──>  预处理  ──>  编译  ──>  汇编  ──>  链接   │
│              │       │          │         │         │         │
│              │       ▼          ▼         ▼         ▼         │
│              │    hello.i   hello.s   hello.o   hello.exe    │
│              │                                                │
│              │    预处理后的源文件  汇编文件  目标文件  可执行文件 │
│              │                                                │
└────────────────────────────────────────────────────────────────┘
```

**各阶段说明：**

| 阶段 | 说明 |
|------|------|
| 预处理 | 处理#include、#define等预处理指令 |
| 编译 | 将C代码转换为汇编代码，进行语法检查 |
| 汇编 | 将汇编代码转换为机器码，生成目标文件(.o) |
| 链接 | 将目标文件与库函数链接，生成可执行文件(.exe) |

---

## 第二章 开发环境

### 2.1 常用开发环境

| 环境 | 平台 | 说明 |
|------|------|------|
| Visual Studio | Windows | 微软开发的完整IDE，功能强大 |
| Code::Blocks | 跨平台 | 轻量级，支持多种编译器 |
| Dev-C++ | Windows | 适合初学者 |
| CLion | 跨平台 | JetBrains出品，需配置MinGW |
| VS Code | 跨平台 | 轻量级编辑器，需配置C环境 |
| Keil MDK | Windows | 专为单片机开发 |

### 2.2 GCC编译器

GCC（GNU Compiler Collection）是开源的编译器套件。

**常用命令：**

```bash
# 编译源代码
gcc source.c -o program

# 指定警告级别
gcc -Wall source.c -o program

# 开启所有警告
gcc -Wextra source.c -o program

# 生成调试信息
gcc -g source.c -o program

# 预处理
gcc -E source.c -o source.i

# 只编译不链接
gcc -c source.c -o source.o
```

### 2.3 Code::Blocks配置

1. 下载安装 Code::Blocks（包含MinGW）
2. 创建新项目：File → New → Project → Console Application
3. 选择C语言
4. 编写代码
5. 按F9编译运行

### 2.4 VS Code配置C环境

**安装扩展：**
- C/C++（微软官方）
- Code Runner

**配置tasks.json：**

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: gcc.exe 生成活动文件",
            "command": "gcc",
            "args": [
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "${workspaceFolder}"
            },
            "problemMatcher": ["$gcc"],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

---

## 第三章 基本语法

### 3.1 C语言基本结构

```c
/*
 * C程序基本结构
 */
#include <stdio.h>      // 头文件包含

#define MAX 100         // 宏定义

// 函数声明
int add(int a, int b);

// 全局变量
int global_var = 10;

// 主函数
int main() {
    // 局部变量
    int num = 50;
    
    // 函数调用
    int result = add(num, global_var);
    
    printf("Result: %d\n", result);
    
    return 0;
}

// 函数定义
int add(int a, int b) {
    return a + b;
}
```

### 3.2 标识符命名规则

**标识符**：用来命名变量、函数、数组等的符号

**命名规则：**
1. 由字母、数字和下划线组成
2. 第一个字符必须是字母或下划线
3. 区分大小写
4. 不能使用关键字
5. 长度没有限制，但编译器通常只识别前31个字符

**正确示例：**
```c
int age;           // 正确
int student_age;   // 正确
int _private;      // 正确（但不建议）
int age2;          // 正确
```

**错误示例：**
```c
int 2age;          // 错误：数字开头
int student-age;    // 错误：包含非法字符-
int int;           // 错误：使用关键字
```

### 3.3 关键字

C语言共有32个关键字（ANSI C标准）：

| 关键字 | 说明 |
|--------|------|
| auto | 自动变量 |
| break | 跳出循环或switch |
| case | switch语句选项 |
| char | 字符型 |
| const | 常量 |
| continue | 继续循环 |
| default | switch默认选项 |
| do | do-while循环 |
| double | 双精度浮点型 |
| else | if-else语句 |
| enum | 枚举 |
| extern | 外部变量声明 |
| float | 单精度浮点型 |
| for | for循环 |
| goto | 无条件跳转 |
| if | 条件语句 |
| int | 整型 |
| long | 长整型 |
| register | 寄存器变量 |
| return | 返回 |
| short | 短整型 |
| signed | 有符号 |
| sizeof | 计算大小 |
| static | 静态变量 |
| struct | 结构体 |
| switch | 多分支语句 |
| typedef | 类型定义 |
| union | 共用体 |
| unsigned | 无符号 |
| void | 空类型 |
| volatile | 易失变量 |
| while | while循环 |

### 3.4 注释

**单行注释：** `// 注释内容`

```c
int a = 10;  // 这是单行注释
```

**多行注释：** `/* 注释内容 */`

```c
/*
 * 这是一个多行注释
 * 可以写很多行
 */
int b = 20;
```

### 3.5 语句与分号

C语言中，每个语句以分号`;`结束。

```c
int a = 10;      // 语句1
int b = 20;      // 语句2
a = a + b;       // 语句3
printf("%d", a); // 语句4
```

### 3.6 代码块

用一对大括号`{ }`括起来的代码形成一个复合语句（代码块）。

```c
{
    int a = 10;
    int b = 20;
    int sum = a + b;
    printf("Sum = %d\n", sum);
}
```

---

## 第四章 数据类型

### 4.1 数据类型分类

```
┌─────────────────────────────────────────────────────────────────┐
│                        C语言数据类型                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    基本类型                                │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐│   │
│  │  │ 整型      │ │ 字符型   │ │ 实型     │ │ 枚举型   ││   │
│  │  │ int      │ │ char     │ │ float    │ │ enum     ││   │
│  │  │ short    │ │          │ │ double   │ │          ││   │
│  │  │ long     │ │          │ │ long     │ │          ││   │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘│   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    构造类型                                │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐              │   │
│  │  │ 数组      │ │ 结构体   │ │ 共用体   │              │   │
│  │  │ array    │ │ struct   │ │ union    │              │   │
│  │  └──────────┘ └──────────┘ └──────────┘              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    指针类型                                │   │
│  │  ┌──────────────────────────────────────────────────┐ │   │
│  │  │                 指针类型                            │ │   │
│  │  │                     *                             │ │   │
│  │  └──────────────────────────────────────────────────┘ │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    空类型                                │   │
│  │  ┌──────────────────────────────────────────────────┐ │   │
│  │  │                 void                               │ │   │
│  │  └──────────────────────────────────────────────────┘ │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 4.2 整型

| 类型 | 说明 | 占字节数 | 取值范围 |
|------|------|----------|----------|
| char | 字符型 | 1 | -128 ~ 127 或 0 ~ 255 |
| short | 短整型 | 2 | -32768 ~ 32767 |
| int | 整型 | 4 | -2147483648 ~ 2147483647 |
| long | 长整型 | 4 | 与int相同（Windows）<br>与系统相关（Linux） |
| long long | 长长整型 | 8 | -9223372036854775808 ~ 9223372036854775807 |

**有符号与无符号：**

```c
/* 有符号整型（默认） */
int a = -10;
signed int b = -20;

/* 无符号整型 */
unsigned int c = 100;
unsigned char d = 255;
```

### 4.3 浮点型

| 类型 | 说明 | 占字节数 | 取值范围 | 精度 |
|------|------|----------|----------|------|
| float | 单精度 | 4 | ±3.4E-38 ~ ±3.4E38 | 6-7位有效数字 |
| double | 双精度 | 8 | ±1.7E-308 ~ ±1.7E308 | 15-16位有效数字 |
| long double | 长双精度 | 16 | 更高 | 更高 |

**示例：**

```c
float f = 3.14f;       // 加f后缀表示float类型
double d = 3.14159;    // 默认double类型
long double ld = 3.1415926535L;  // 加L后缀表示long double
```

### 4.4 字符型

字符型用于存储单个字符，本质上是1字节的整型。

```c
char c1 = 'A';           // 字符常量
char c2 = 65;           // ASCII码值
char c3 = '\n';          // 转义字符
char c4 = '\t';          // 制表符

printf("c1 = %c, ASCII = %d\n", c1, c1);  // c1 = A, ASCII = 65
```

### 4.5 sizeof运算符

`sizeof`用于计算数据类型或变量占用的字节数。

```c
#include <stdio.h>

int main() {
    printf("char: %d bytes\n", sizeof(char));        // 1
    printf("int: %d bytes\n", sizeof(int));          // 4
    printf("float: %d bytes\n", sizeof(float));      // 4
    printf("double: %d bytes\n", sizeof(double));     // 8
    printf("long: %d bytes\n", sizeof(long));         // 4或8
    
    int a = 10;
    printf("a: %d bytes\n", sizeof(a));              // 4
    
    return 0;
}
```

### 4.6 数据类型转换

**自动转换（隐式转换）：**

当不同类型的数据混合运算时，低精度类型自动转换为高精度类型。

```
char → short → int → long → float → double
              ↑
        unsigned
```

```c
int a = 10;
double b = 3.14;
double c = a + b;  // a自动转换为double后相加
```

**强制转换（显式转换）：**

使用强制类型转换运算符`(类型)`进行转换。

```c
int a = 10, b = 3;
double c = (double)a / b;  // 强制转换为double: c = 3.333...
double d = a / b;          // 隐式转换: d = 3.0 (整数除法)
```

---

## 第五章 变量与常量

### 5.1 变量

**变量**：在程序执行过程中值可以改变的量。

**定义格式：**
```c
类型说明符 变量名1, 变量名2, ...;
```

**示例：**
```c
int age;                  // 定义整型变量age
float price = 9.99;      // 定义并初始化
char grade = 'A';
double pi = 3.14159;
```

### 5.2 变量的分类

| 分类方式 | 类型 | 说明 | 生命周期 | 作用域 |
|----------|------|------|----------|--------|
| 按存储类型 | 自动变量 | 函数内部定义 | 函数结束 | 函数内 |
| | 静态变量 | 用static修饰 | 程序结束 | 定义位置 |
| | 寄存器变量 | 用register修饰 | 函数结束 | 函数内 |
| | 外部变量 | 函数外部定义 | 程序结束 | 全局 |

**自动变量：**
```c
void func() {
    int count = 0;  // 自动变量，每次调用都重新初始化
    count++;
    printf("count = %d\n", count);
}
```

**静态变量：**
```c
void func() {
    static int count = 0;  // 静态变量，只初始化一次，值保留
    count++;
    printf("count = %d\n", count);
}

int main() {
    func();  // count = 1
    func();  // count = 2
    func();  // count = 3
    return 0;
}
```

### 5.3 常量

**常量**：在程序执行过程中值不能改变的量。

**常量类型：**

| 类型 | 示例 |
|------|------|
| 整型常量 | 10, 0, -25, 0xFF (十六进制), 0177 (八进制) |
| 浮点型常量 | 3.14, 2.5e-3, 0.314E1 |
| 字符常量 | 'a', 'A', '\n', '\t' |
| 字符串常量 | "Hello", "world" |
| 标识符常量 | #define MAX 100 |

### 5.4 const修饰符

`const`用于定义常量，其值不能修改。

```c
const int MAX = 100;
const float PI = 3.14159;

// MAX = 200;  // 错误！不能修改const常量的值

// const修饰指针
const int *p1;      // 指向常量的指针，不能通过p1修改指向的值
int const *p2;      // 同上
int * const p3;     // 常指针，指针本身不能改变
const int * const p4;  // 指向常量的常指针
```

### 5.5 宏定义

使用 `#define` 定义宏常量。

```c
#define MAX 100
#define PI 3.14159
#define NAME "MyProgram"
#define TRUE 1
#define FALSE 0

int main() {
    int array[MAX];  // 相当于 int array[100];
    printf("PI = %.5f\n", PI);
    return 0;
}
```

**宏定义与const的区别：**

| 特性 | #define | const |
|------|---------|-------|
| 类型 | 无类型 | 有类型 |
| 内存 | 不分配内存（预处理替换） | 分配内存 |
| 调试 | 替换后无法调试 | 可以调试 |
| 作用域 | 全局 | 有作用域 |

### 5.6 枚举类型

枚举类型用于定义一组命名的整型常量。

```c
enum Weekday {
    MONDAY,    // 0
    TUESDAY,   // 1
    WEDNESDAY, // 2
    THURSDAY,  // 3
    FRIDAY,    // 4
    SATURDAY,  // 5
    SUNDAY     // 6
};

enum Weekday today = MONDAY;
```

**指定枚举值：**
```c
enum Status {
    SUCCESS = 0,
    ERROR = -1,
    WARNING = 1,
    INFO = 2
};
```

---

## 第六章 运算符与表达式

### 6.1 运算符分类

```
┌─────────────────────────────────────────────────────────────────┐
│                        C语言运算符                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐      │
│  │ 算术运算符 │ │ 关系运算符 │ │ 逻辑运算符 │ │ 位运算符  │      │
│  │ + - * / % │ │ > < == != │ │ && || !  │ │ & | ^ ~  │      │
│  └───────────┘ └───────────┘ └───────────┘ └───────────┘      │
│                                                                 │
│  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐      │
│  │ 赋值运算符 │ │ 条件运算符 │ │ 逗号运算符 │ │sizeof运算符│      │
│  │ = += -=   │ │ ?:        │ │ ,         │ │ sizeof   │      │
│  └───────────┘ └───────────┘ └───────────┘ └───────────┘      │
│                                                                 │
│  ┌───────────┐ ┌───────────┐                                   │
│  │ 自增自减  │ │ 指针运算符 │                                   │
│  │ ++ --    │ │ * &      │                                   │
│  └───────────┘ └───────────┘                                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 6.2 算术运算符

| 运算符 | 说明 | 示例 |
|--------|------|------|
| + | 加 | a + b |
| - | 减 | a - b |
| * | 乘 | a * b |
| / | 除 | a / b |
| % | 取余 | a % b |

**示例：**
```c
int a = 10, b = 3;
printf("%d\n", a + b);  // 13
printf("%d\n", a - b);  // 7
printf("%d\n", a * b);   // 30
printf("%d\n", a / b);   // 3 (整数除法)
printf("%d\n", a % b);   // 1 (取余)
```

### 6.3 自增自减运算符

| 运算符 | 说明 | 示例 |
|--------|------|------|
| ++ | 自增1 | a++ 或 ++a |
| -- | 自减1 | a-- 或 --a |

**前置与后置的区别：**
```c
int a = 5, b, c;

b = ++a;  // a先自增为6，再赋值给b: a=6, b=6
c = a++;  // a的值6先赋值给c，再自增: a=7, c=6
```

### 6.4 关系运算符

| 运算符 | 说明 | 示例 |
|--------|------|------|
| > | 大于 | a > b |
| >= | 大于等于 | a >= b |
| < | 小于 | a < b |
| <= | 小于等于 | a <= b |
| == | 等于 | a == b |
| != | 不等于 | a != b |

**示例：**
```c
int a = 5, b = 3;
printf("%d\n", a > b);   // 1 (真)
printf("%d\n", a == b);  // 0 (假)
printf("%d\n", a != b);  // 1 (真)
```

### 6.5 逻辑运算符

| 运算符 | 说明 | 示例 |
|--------|------|------|
| && | 逻辑与 | a && b |
| \|\| | 逻辑或 | a \|\| b |
| ! | 逻辑非 | !a |

**真值表：**

| A | B | A && B | A \|\| B | !A |
|---|---|--------|----------|-----|
| 真 | 真 | 真 | 真 | 假 |
| 真 | 假 | 假 | 真 | 假 |
| 假 | 真 | 假 | 真 | 真 |
| 假 | 假 | 假 | 假 | 真 |

**短路特性：**
```c
// &&：左边为假，右边不执行
if (a != 0 && b / a > 5)  // 避免除零错误

// ||：左边为真，右边不执行
if (p == NULL || strcmp(p, "end") == 0)  // 避免空指针访问
```

### 6.6 赋值运算符

**简单赋值：**
```c
int a = 10;
a = 20;
```

**复合赋值：**
```c
int a = 10;
a += 5;   // a = a + 5 = 15
a -= 3;   // a = a - 3 = 12
a *= 2;   // a = a * 2 = 24
a /= 4;   // a = a / 4 = 6
a %= 4;   // a = a % 4 = 2
```

### 6.7 条件运算符

**语法：** `表达式1 ? 表达式2 : 表达式3`

```c
// 求最大值
int a = 10, b = 20;
int max = (a > b) ? a : b;  // max = 20

// 求最小值
int min = (a < b) ? a : b;   // min = 10

// 求绝对值
int x = -5;
int abs_x = (x > 0) ? x : -x;  // abs_x = 5
```

### 6.8 逗号运算符

逗号运算符用于连接多个表达式，从左到右依次计算。

```c
int a = (1, 2, 3);  // a = 3（取最后一个表达式的值）

// 逗号表达式常见用法
for (int i = 0, j = 10; i < j; i++, j--) {
    printf("i=%d, j=%d\n", i, j);
}
```

### 6.9 运算符优先级

| 优先级 | 运算符 | 结合性 |
|--------|--------|--------|
| 1 | () [] . -> | 左到右 |
| 2 | ! ~ ++ -- + - * & sizeof | 右到左 |
| 3 | * / % | 左到右 |
| 4 | + - | 左到右 |
| 5 | << >> | 左到右 |
| 6 | < <= > >= | 左到右 |
| 7 | == != | 左到右 |
| 8 | & | 左到右 |
| 9 | ^ | 左到右 |
| 10 | \| | 左到右 |
| 11 | && | 左到右 |
| 12 | \|\| | 左到右 |
| 13 | ?: | 右到左 |
| 14 | = += -= *= /= %= &= ^= \|= <<= >>= | 右到左 |
| 15 | , | 左到右 |

---

## 第七章 程序结构

### 7.1 顺序结构

顺序结构是C语言的基本结构，语句按书写顺序依次执行。

```c
int main() {
    int a = 10, b = 20;
    int sum = a + b;      // 先执行加法
    printf("%d\n", sum);  // 再输出结果
    return 0;
}
```

**求圆的周长和面积：**
```c
#include <stdio.h>

int main() {
    int r = 3;
    float L, S;
    const float PI = 3.14;
    
    L = 2 * PI * r;      // 计算周长
    S = PI * r * r;      // 计算面积
    
    printf("半径是%d的圆的周长是%.2f，面积是%.2f\n", r, L, S);
    
    return 0;
}
```

### 7.2 代码格式化

**好的代码风格：**
```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 20;
    int sum = a + b;
    
    if (a > b) {
        printf("a is greater than b\n");
    } else {
        printf("b is greater than or equal to a\n");
    }
    
    return 0;
}
```

**代码缩进：**
- 每嵌套一层，缩进增加一级（通常4个空格或1个Tab）
- 函数体、循环体、if/else体都要缩进

---

## 第八章 选择结构

### 8.1 if语句

**基本格式：**
```c
if (条件表达式) {
    // 条件为真时执行的语句
}
```

**示例：**
```c
int score = 85;
if (score >= 60) {
    printf("及格了！\n");
}
```

### 8.2 if-else语句

**基本格式：**
```c
if (条件表达式) {
    // 条件为真时执行的语句
} else {
    // 条件为假时执行的语句
}
```

**示例：**
```c
int num = 10;
if (num % 2 == 0) {
    printf("%d是偶数\n", num);
} else {
    printf("%d是奇数\n", num);
}
```

### 8.3 if-else if-else语句

**基本格式：**
```c
if (条件1) {
    // 条件1为真时执行的语句
} else if (条件2) {
    // 条件2为真时执行的语句
} else if (条件3) {
    // 条件3为真时执行的语句
} else {
    // 所有条件都不满足时执行的语句
}
```

**成绩等级判断：**
```c
#include <stdio.h>

int main() {
    float score;
    printf("请输入小明的成绩：");
    scanf("%f", &score);
    
    if (score >= 90) {
        printf("获得大餐一顿！\n");
    } else if (score >= 70) {
        printf("获得篮球一个！\n");
    } else if (score >= 60) {
        printf("获得练习册一本！\n");
    } else {
        printf("获得大嘴巴子一个！\n");
    }
    
    return 0;
}
```

### 8.4 嵌套if语句

在if或else分支中再包含if语句。

```c
int score = 85;
int attendance = 90;

if (score >= 60) {
    if (attendance >= 90) {
        printf("优秀！\n");
    } else if (attendance >= 70) {
        printf("良好！\n");
    } else {
        printf("及格！\n");
    }
} else {
    printf("不及格！\n");
}
```

### 8.5 switch语句

**基本格式：**
```c
switch (表达式) {
    case 常量1:
        // 语句1
        break;
    case 常量2:
        // 语句2
        break;
    ...
    default:
        // 默认语句
        break;
}
```

**成绩等级判断：**
```c
#include <stdio.h>

int main() {
    char grade;
    printf("请输入成绩等级(A/B/C/D)：");
    scanf("%c", &grade);
    
    switch (grade) {
        case 'A':
            printf("90-100分\n");
            break;
        case 'B':
            printf("80-89分\n");
            break;
        case 'C':
            printf("70-79分\n");
            break;
        case 'D':
            printf("60-69分\n");
            break;
        default:
            printf("输入错误！\n");
            break;
    }
    
    return 0;
}
```

**注意：**
- case后的值必须是常量或常量表达式
- case后的值必须互不相同
- break用于跳出switch，否则会"贯穿"
- default可选，用于处理所有case都不匹配的情况

### 8.6 switch的贯穿特性

```c
switch (grade) {
    case 'A':
    case 'B':
    case 'C':
        printf("及格\n");
        break;
    case 'D':
        printf("不及格\n");
        break;
}
```

---

## 第九章 循环结构

### 9.1 while循环

**基本格式：**
```c
while (条件表达式) {
    // 循环体
}
```

**流程图：**
```
┌─────────────────┐
│                 │
│    开始         │
│      ↓         │
│  ┌─────────┐   │
│  │ 条件判断 │   │
│  └───┬─────┘   │
│      ↓         │
│   ┌───────┐    │
│   │ 条件   │    │
│   │ 为真？  │    │
│   └───┬───┘    │
│      ↓│        │
│   ┌──┴──┐     │
│   │ 执行  │     │
│   │ 循环体│     │
│   └──┬───┘     │
│      │         │
│      └─────────┘
│      ↓(否)     │
│      ↓         │
│   结束         │
└─────────────────┘
```

**示例：计算1到100的和**
```c
#include <stdio.h>

int main() {
    int i = 1;
    int sum = 0;
    
    while (i <= 100) {
        sum += i;
        i++;
    }
    
    printf("1+2+...+100 = %d\n", sum);
    return 0;
}
```

### 9.2 do-while循环

**基本格式：**
```c
do {
    // 循环体
} while (条件表达式);
```

**特点：** 先执行循环体，再判断条件，循环体至少执行一次。

**示例：**
```c
#include <stdio.h>

int main() {
    int num;
    
    do {
        printf("请输入一个正整数：");
        scanf("%d", &num);
    } while (num <= 0);
    
    printf("你输入了：%d\n", num);
    return 0;
}
```

### 9.3 for循环

**基本格式：**
```c
for (初始化; 条件; 更新) {
    // 循环体
}
```

**执行顺序：** 初始化 → 条件判断 → 循环体 → 更新 → 条件判断 → ...

**示例：计算1到100的和**
```c
#include <stdio.h>

int main() {
    int sum = 0;
    
    for (int i = 1; i <= 100; i++) {
        sum += i;
    }
    
    printf("1+2+...+100 = %d\n", sum);
    return 0;
}
```

### 9.4 for循环的多种形式

```c
// 形式1：标准形式
for (int i = 0; i < 10; i++) {
    printf("%d ", i);
}

// 形式2：初始化在外部
int i = 0;
for (; i < 10; i++) {
    printf("%d ", i);
}

// 形式3：更新在循环体内部
for (int i = 0; i < 10;) {
    printf("%d ", i);
    i++;
}

// 形式4：死循环
for (;;) {
    // 无限循环，需要配合break使用
}

// 形式5：多个变量
for (int i = 0, j = 10; i < j; i++, j--) {
    printf("i=%d, j=%d\n", i, j);
}
```

### 9.5 嵌套循环

循环内部再包含循环。

**打印九九乘法表：**
```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 9; i++) {
        for (int j = 1; j <= i; j++) {
            printf("%d*%d=%2d ", j, i, i*j);
        }
        printf("\n");
    }
    return 0;
}
```

**输出：**
```
1*1= 1 
1*2= 2 2*2= 4 
1*3= 3 2*3= 6 3*3= 9 
...
```

### 9.6 break语句

`break`用于跳出最近的循环（while、for、do-while）或switch。

```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 10; i++) {
        if (i == 5) {
            break;  // 当i等于5时跳出循环
        }
        printf("%d ", i);
    }
    return 0;
}
// 输出：1 2 3 4
```

### 9.7 continue语句

`continue`用于跳过本次循环的剩余部分，进入下一次循环。

```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 10; i++) {
        if (i == 5 || i == 7) {
            continue;  // 跳过5和7
        }
        printf("%d ", i);
    }
    return 0;
}
// 输出：1 2 3 4 6 8 9 10
```

### 9.8 循环经典示例

**示例1：判断素数**
```c
#include <stdio.h>

int main() {
    int num;
    printf("请输入一个正整数：");
    scanf("%d", &num);
    
    int is_prime = 1;
    for (int i = 2; i * i <= num; i++) {
        if (num % i == 0) {
            is_prime = 0;
            break;
        }
    }
    
    if (is_prime && num > 1) {
        printf("%d是素数\n", num);
    } else {
        printf("%d不是素数\n", num);
    }
    
    return 0;
}
```

**示例2：斐波那契数列**
```c
#include <stdio.h>

int main() {
    int n;
    printf("请输入项数：");
    scanf("%d", &n);
    
    int a = 0, b = 1, c;
    printf("斐波那契数列前%d项：\n", n);
    
    for (int i = 0; i < n; i++) {
        printf("%d ", a);
        c = a + b;
        a = b;
        b = c;
    }
    
    return 0;
}
```

**示例3：水仙花数**
```c
#include <stdio.h>

int main() {
    printf("水仙花数有：\n");
    
    for (int i = 100; i <= 999; i++) {
        int a = i / 100;       // 百位
        int b = i / 10 % 10;   // 十位
        int c = i % 10;        // 个位
        
        if (a*a*a + b*b*b + c*c*c == i) {
            printf("%d ", i);
        }
    }
    
    return 0;
}
// 输出：153 370 371 407
```

---

## 第十章 数组

### 10.1 数组的概念

数组是相同类型数据的有序集合，用一个名字和下标来访问各个元素。

```
数组名: arr
下标:   [0] [1] [2] [3] [4] [5] ...
值:      10  20  30  40  50  60  ...
```

### 10.2 一维数组

**定义格式：**
```c
类型说明符 数组名[数组长度];
```

**示例：**
```c
int scores[5];          // 定义5个整型元素的数组
float prices[10];       // 定义10个浮点型元素的数组
char name[20];           // 定义20个字符型元素的数组
```

**初始化：**
```c
// 完全初始化
int arr1[5] = {1, 2, 3, 4, 5};

// 部分初始化（未初始化的元素自动为0）
int arr2[5] = {1, 2};   // arr2 = {1, 2, 0, 0, 0}

// 省略数组长度（编译器自动计算）
int arr3[] = {1, 2, 3, 4, 5};  // 长度为5

// 所有元素初始化为0
int arr4[5] = {0};      // arr4 = {0, 0, 0, 0, 0}
```

### 10.3 数组元素的访问

数组元素通过下标访问，下标从0开始。

```c
int arr[5] = {10, 20, 30, 40, 50};

printf("%d\n", arr[0]);  // 10 (第一个元素)
printf("%d\n", arr[4]);  // 50 (最后一个元素)
printf("%d\n", arr[5]);  // 越界访问！危险！

// 修改元素
arr[2] = 100;  // arr = {10, 20, 100, 40, 50}
```

### 10.4 数组的输入输出

```c
#include <stdio.h>

int main() {
    int n;
    printf("请输入数组元素个数：");
    scanf("%d", &n);
    
    int arr[100];
    
    // 输入
    printf("请输入%d个整数：\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    // 输出
    printf("数组元素为：\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

### 10.5 数组作为函数参数

数组作为函数参数时，实际传递的是数组首地址。

```c
// 方式1：指定长度
void printArray(int arr[10], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// 方式2：不指定长度
void printArray2(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// 方式3：使用指针
void printArray3(int *arr, int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}
```

### 10.6 二维数组

**定义格式：**
```c
类型说明符 数组名[行数][列数];
```

**示例：**
```c
int matrix[3][4];      // 3行4列的整型数组
float scores[5][3];    // 5个学生3门课的成绩
```

**初始化：**
```c
// 完全初始化
int a[2][3] = {{1, 2, 3}, {4, 5, 6}};

// 部分初始化
int b[2][3] = {{1, 2}, {4}};  // b = {{1, 2, 0}, {4, 0, 0}}

// 省略第一维
int c[][3] = {{1, 2, 3}, {4, 5, 6}};  // 自动计算为2行
```

**内存存储：**
```
按行存储：
[0][0] [0][1] [0][2] [1][0] [1][1] [1][2]
   1       2       3       4       5       6
```

### 10.7 二维数组示例

**矩阵相乘：**
```c
#include <stdio.h>

int main() {
    int A[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int B[3][2] = {{1, 2}, {3, 4}, {5, 6}};
    int C[2][2] = {0};
    
    // 矩阵乘法 C = A * B
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            for (int k = 0; k < 3; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    
    // 输出结果
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            printf("%d ", C[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

### 10.8 字符数组与字符串

字符数组用于存储字符，字符串是字符数组以'\0'结尾。

```c
// 字符数组
char c1[] = {'H', 'e', 'l', 'l', 'o'};  // 没有'\0'
char c2[] = {'H', 'e', 'l', 'l', 'o', '\0'};  // 有'\0'

// 字符串
char s1[] = "Hello";  // 自动包含'\0'
char s2[20] = "World";
```

**字符串输入输出：**
```c
char name[50];

// 使用scanf（遇到空格停止）
scanf("%s", name);  // 不需要&，数组名就是地址

// 使用gets（危险，不推荐）
gets(name);  // 可能溢出

// 使用fgets（推荐）
fgets(name, sizeof(name), stdin);  // 安全
```

---

## 第十一章 函数

### 11.1 函数的概念

函数是一段具有特定功能的代码块，可以被多次调用。

```
┌─────────────────────────────────────────────────────────────┐
│                        函数调用流程                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  main函数 ──> 调用add() ──> 执行add() ──> 返回main函数    │
│                │                    │                         │
│                │  传递参数          │  返回值                 │
│                ↓                    ↓                         │
│            ┌───────────┐      ┌───────────┐                │
│            │   add()   │      │   add()   │                │
│            │  int a,b  │      │  return   │                │
│            │  return   │      │    a+b    │                │
│            │   a+b     │      │           │                │
│            └───────────┘      └───────────┘                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 11.2 函数的定义

**格式：**
```c
返回类型 函数名(参数列表) {
    // 函数体
    return 返回值;
}
```

**示例：**
```c
// 求最大值
int max(int a, int b) {
    return (a > b) ? a : b;
}

// 求阶乘
long long factorial(int n) {
    long long result = 1;
    for (int i = 1; i <= n; i++) {
        result *= i;
    }
    return result;
}

// 无返回值
void printHello() {
    printf("Hello!\n");
}

// 无参数无返回值
void wait() {
    printf("请按任意键继续...\n");
    getchar();
}
```

### 11.3 函数的声明

函数的声明（原型）告诉编译器函数的存在。

```c
#include <stdio.h>

// 函数声明（可选，但推荐）
int max(int a, int b);
void swap(int *x, int *y);

// 主函数
int main() {
    int a = 10, b = 20;
    printf("最大值：%d\n", max(a, b));
    
    swap(&a, &b);
    printf("交换后：a=%d, b=%d\n", a, b);
    return 0;
}

// 函数定义
int max(int a, int b) {
    return (a > b) ? a : b;
}

void swap(int *x, int *y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}
```

### 11.4 函数的调用

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {
    int x = 10, y = 20;
    int sum;
    
    // 作为表达式
    sum = add(x, y);
    printf("%d + %d = %d\n", x, y, sum);
    
    // 作为语句
    add(x, y);  // 返回值被忽略
    
    // 作为参数
    printf("结果：%d\n", add(add(1, 2), 3));  // 嵌套调用
    
    return 0;
}
```

### 11.5 参数传递

**值传递：**
```c
void swap(int x, int y) {
    int temp = x;
    x = y;
    y = temp;
}

int main() {
    int a = 10, b = 20;
    swap(a, b);  // a和b不变！因为传递的是值的拷贝
    printf("a=%d, b=%d\n", a, b);  // a=10, b=20
    return 0;
}
```

**地址传递：**
```c
void swap(int *x, int *y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}

int main() {
    int a = 10, b = 20;
    swap(&a, &b);  // 传递地址，可以改变a和b的值
    printf("a=%d, b=%d\n", a, b);  // a=20, b=10
    return 0;
}
```

### 11.6 递归函数

递归函数是调用自身的函数，需要有终止条件。

**阶乘递归：**
```c
long long factorial(int n) {
    if (n <= 1) {
        return 1;  // 终止条件
    }
    return n * factorial(n - 1);  // 递归调用
}
```

**递归执行过程（factorial(5)）：**
```
factorial(5)
  → 5 * factorial(4)
        → 4 * factorial(3)
              → 3 * factorial(2)
                    → 2 * factorial(1)
                          → 1
                    ← 返回 1
              ← 返回 2 * 1 = 2
        ← 返回 3 * 2 = 6
  ← 返回 4 * 6 = 24
← 返回 5 * 24 = 120
```

**汉诺塔问题：**
```c
#include <stdio.h>

void hanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", from, to);
        return;
    }
    hanoi(n - 1, from, aux, to);
    printf("Move disk %d from %c to %c\n", n, from, to);
    hanoi(n - 1, aux, to, from);
}

int main() {
    int n = 3;
    hanoi(n, 'A', 'C', 'B');
    return 0;
}
```

### 11.7 变量的作用域

| 类型 | 关键字 | 生命周期 | 作用域 |
|------|--------|----------|--------|
| 自动变量 | (默认) | 函数结束 | 函数内 |
| 静态变量 | static | 程序结束 | 定义位置 |
| 寄存器变量 | register | 函数结束 | 函数内 |
| 外部变量 | extern | 程序结束 | 全局 |
| 静态外部变量 | static | 程序结束 | 定义文件内 |

### 11.8 内部函数与外部函数

```c
// 文件1.c
static void internalFunc();  // 静态（内部）函数，只能在本文件使用
extern void externalFunc();   // 外部函数，可被其他文件调用

// 文件2.c
extern void externalFunc();   // 声明使用外部函数
```

---

## 第十二章 指针

### 12.1 指针的概念

**指针**是存放变量地址的变量。

```
┌─────────────────────────────────────────────────────────────┐
│                        指针示意图                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│    变量a         指针变量p                                 │
│   ┌──────┐       ┌────────┐                               │
│   │      │       │        │                               │
│   │ 100  │◄──────│ 0x1000 │  p存放a的地址                   │
│   │      │       │        │                               │
│   └──────┘       └────────┘                               │
│   地址:0x1000    地址:0x2000                               │
│                                                             │
│   p = &a;     // p指向a                                    │
│   *p = 200;   // 通过p修改a的值                           │
│   printf("%d", a);  // 输出200                              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 12.2 指针的定义与使用

```c
int a = 10;
int *p;      // 定义整型指针p

p = &a;     // p指向a（&是取地址运算符）

printf("%d\n", a);    // 输出10
printf("%d\n", *p);  // 输出10（*是指针运算符，访问指针指向的值）

*p = 200;    // 通过指针修改a的值
printf("%d\n", a);    // 输出200
```

### 12.3 指针的初始化

```c
int a = 10;
int *p = &a;     // 定义时初始化

// 指向常量
int *p1 = NULL;  // NULL表示空指针，不指向任何地址

// 不同类型指针
char *pc;
float *pf;
double *pd;
```

### 12.4 指针运算

| 运算 | 说明 |
|------|------|
| p++ / ++p | 指针向后移动一个数据单位 |
| p-- / --p | 指针向前移动一个数据单位 |
| p + n / p - n | 指针向后/前移动n个数据单位 |
| p1 - p2 | 两个同类型指针的距离 |
| p1 == p2 | 判断两个指针是否相等 |

```c
int arr[5] = {10, 20, 30, 40, 50};
int *p = arr;  // p指向arr[0]

printf("%d\n", *p);    // 10
printf("%d\n", *(p+1)); // 20
printf("%d\n", *(p+2)); // 30

p += 2;  // p指向arr[2]
printf("%d\n", *p);    // 30
```

### 12.5 指针与数组

数组名就是数组首元素的地址。

```c
int arr[5] = {10, 20, 30, 40, 50};
int *p = arr;  // 等价于 int *p = &arr[0];

// 两种访问方式等价
for (int i = 0; i < 5; i++) {
    printf("%d ", arr[i]);   // 下标方式
    printf("%d ", *(p + i)); // 指针方式
    printf("%d ", *(arr + i)); // 数组名+偏移
}
```

### 12.6 指针数组

指针数组是数组，每个元素都是指针。

```c
int a = 10, b = 20, c = 30;
int *p[3] = {&a, &b, &c};

printf("%d\n", *p[0]);  // 10
printf("%d\n", *p[1]);  // 20
printf("%d\n", *p[2]);  // 30
```

### 12.7 指向指针的指针

二级指针是指向指针的指针。

```c
int a = 10;
int *p1 = &a;      // p1是指向a的指针
int **p2 = &p1;     // p2是指向p1的指针

printf("%d\n", a);     // 10
printf("%d\n", *p1);   // 10
printf("%d\n", **p2);  // 10
```

### 12.8 函数指针

函数指针是指向函数的指针。

```c
int add(int a, int b) {
    return a + b;
}

int sub(int a, int b) {
    return a - b;
}

int main() {
    int (*p)(int, int);  // 定义函数指针
    p = add;              // 指向add函数
    printf("%d\n", p(10, 5));  // 15
    
    p = sub;              // 指向sub函数
    printf("%d\n", p(10, 5));  // 5
    
    return 0;
}
```

### 12.9 指针与字符串

```c
// 字符指针
char *p = "Hello";  // p指向字符串常量

// 字符数组
char arr[] = "Hello";  // 数组，内容可以修改

// 区别
p[0] = 'h';  // 危险！字符串常量不可修改
arr[0] = 'h'; // 正确

// 字符串拷贝
void strcpy(char *dest, const char *src) {
    while (*src != '\0') {
        *dest = *src;
        dest++;
        src++;
    }
    *dest = '\0';
}
```

### 12.10 const与指针

```c
int a = 10, b = 20;

// 指向常量的指针
const int *p1 = &a;  // 不能通过p1修改a
// p1 = &b;  // 可以改变p1的指向
// *p1 = 100;  // 错误！

// 常指针
int * const p2 = &a;  // 指针本身不能改变
// p2 = &b;  // 错误！
*p2 = 100;  // 可以通过p2修改a

// 指向常量的常指针
const int * const p3 = &a;  // 都不能改变
```

---

## 第十三章 字符串

### 13.1 字符串的概念

字符串是由字符组成的有序序列，以'\0'（空字符）结尾。

```
字符串: H  e  l  l  o  \0
索引:    0  1  2  3  4  5
```

### 13.2 字符串的存储

```c
// 方式1：字符数组
char str1[] = "Hello";
char str2[] = {'H', 'e', 'l', 'l', 'o', '\0'};

// 方式2：字符指针
char *str3 = "Hello";

// 方式3：动态分配
char *str4 = (char *)malloc(6 * sizeof(char));
strcpy(str4, "Hello");
```

### 13.3 字符串输入输出

```c
#include <stdio.h>

int main() {
    char name[50];
    
    // scanf（遇到空格停止）
    printf("请输入姓名：");
    scanf("%s", name);
    printf("Hello, %s!\n", name);
    
    // gets（危险，已废弃）
    // gets(name);  // 可能溢出
    
    // fgets（推荐）
    printf("请输入地址：");
    fgets(name, sizeof(name), stdin);
    name[strcspn(name, "\n")] = '\0';  // 去除换行符
    
    return 0;
}
```

### 13.4 常用字符串函数

| 函数 | 功能 | 头文件 |
|------|------|--------|
| strlen(s) | 求字符串长度 | string.h |
| strcpy(s1, s2) | 拷贝字符串 | string.h |
| strcat(s1, s2) | 连接字符串 | string.h |
| strcmp(s1, s2) | 比较字符串 | string.h |
| strchr(s, c) | 查找字符 | string.h |
| strstr(s1, s2) | 查找子串 | string.h |

**示例：**
```c
#include <stdio.h>
#include <string.h>

int main() {
    char s1[100] = "Hello";
    char s2[] = "World";
    
    // 长度
    printf("长度: %lu\n", strlen(s1));  // 5
    
    // 拷贝
    strcpy(s1, "Hi");
    printf("s1: %s\n", s1);  // Hi
    
    // 连接
    strcat(s1, " ");
    strcat(s1, s2);
    printf("连接: %s\n", s1);  // Hi World
    
    // 比较
    printf("比较: %d\n", strcmp("abc", "abc"));  // 0
    printf("比较: %d\n", strcmp("abc", "abd"));  // -1
    
    // 查找
    char *p = strchr("hello", 'l');
    if (p) printf("找到: %s\n", p);  // llo
    
    return 0;
}
```

### 13.5 字符串数组

字符串数组用于存储多个字符串。

```c
// 二维字符数组
char names[3][20] = {
    "Alice",
    "Bob",
    "Charlie"
};

// 指针数组
char *names[] = {
    "Alice",
    "Bob",
    "Charlie"
};
```

### 13.6 字符串处理示例

**字符串反转：**
```c
#include <stdio.h>
#include <string.h>

void reverseString(char *str) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - 1 - i];
        str[len - 1 - i] = temp;
    }
}

int main() {
    char str[] = "Hello";
    reverseString(str);
    printf("%s\n", str);  // olleH
    return 0;
}
```

**单词统计：**
```c
#include <stdio.h>
#include <string.h>

int countWords(char *str) {
    int count = 0;
    int inWord = 0;
    
    while (*str) {
        if (*str == ' ' || *str == '\t' || *str == '\n') {
            inWord = 0;
        } else if (!inWord) {
            inWord = 1;
            count++;
        }
        str++;
    }
    return count;
}

int main() {
    char str[] = "Hello World C Language";
    printf("单词数: %d\n", countWords(str));  // 4
    return 0;
}
```

---

## 第十四章 结构体

### 14.1 结构体的概念

结构体是用户自定义的数据类型，用于组合不同类型的数据。

```
┌─────────────────────────────────────────────────────────────┐
│                      学生信息结构体                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  struct Student {                                           │
│      char name[20];    // 姓名                             │
│      int age;         // 年龄                             │
│      char gender;     // 性别                             │
│      float score;     // 成绩                             │
│  };                                                        │
│                                                             │
│  ┌──────────────────────────────────────────────────┐    │
│  │  name[20] │ age │ gender │ score                 │    │
│  │  "张三"   │ 18  │   'M'   │ 95.5                  │    │
│  └──────────────────────────────────────────────────┘    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 14.2 结构体的定义与使用

```c
#include <stdio.h>
#include <string.h>

// 定义结构体
struct Student {
    char name[20];
    int age;
    char gender;
    float score;
};

int main() {
    // 定义结构体变量
    struct Student stu1;
    
    // 访问成员并赋值
    strcpy(stu1.name, "张三");
    stu1.age = 18;
    stu1.gender = 'M';
    stu1.score = 95.5;
    
    // 访问成员并输出
    printf("姓名: %s\n", stu1.name);
    printf("年龄: %d\n", stu1.age);
    printf("性别: %c\n", stu1.gender);
    printf("成绩: %.1f\n", stu1.score);
    
    return 0;
}
```

### 14.3 结构体的初始化

```c
// 定义时初始化
struct Student stu1 = {"张三", 18, 'M', 95.5};

// 指定成员初始化（C99）
struct Student stu2 = {
    .name = "李四",
    .age = 19,
    .gender = 'F',
    .score = 88.0
};

// 部分初始化
struct Student stu3 = {"王五", 20};
// stu3.score自动初始化为0.0
```

### 14.4 结构体数组

```c
struct Student students[3] = {
    {"张三", 18, 'M', 95.5},
    {"李四", 19, 'F', 88.0},
    {"王五", 20, 'M', 92.0}
};

// 遍历
for (int i = 0; i < 3; i++) {
    printf("%s %d %c %.1f\n", 
           students[i].name, 
           students[i].age, 
           students[i].gender, 
           students[i].score);
}
```

### 14.5 结构体指针

```c
struct Student stu = {"张三", 18, 'M', 95.5};
struct Student *p = &stu;

// 方式1：使用*访问
printf("%s\n", (*p).name);

// 方式2：使用->访问（更常用）
printf("%s\n", p->name);
printf("%d\n", p->age);
```

### 14.6 typedef与结构体

使用typedef为结构体起别名，简化代码。

```c
// 方式1：不使用typedef
struct Student {
    char name[20];
    int age;
};
struct Student stu1;

// 方式2：使用typedef
typedef struct {
    char name[20];
    int age;
} Student;
Student stu2;

// 方式3：同时有标签和别名
typedef struct StudentInfo {
    char name[20];
    int age;
} Student;
Student stu3;
```

### 14.7 结构体与函数

**结构体作为参数（值传递）：**
```c
void printStudent(struct Student s) {
    printf("%s %d %c %.1f\n", s.name, s.age, s.gender, s.score);
}
```

**结构体指针作为参数（地址传递，推荐）：**
```c
void printStudent(struct Student *p) {
    printf("%s %d %c %.1f\n", p->name, p->age, p->gender, p->score);
}
```

**返回结构体：**
```c
struct Student createStudent(char name[], int age, char gender, float score) {
    struct Student stu;
    strcpy(stu.name, name);
    stu.age = age;
    stu.gender = gender;
    stu.score = score;
    return stu;
}
```

### 14.8 结构体嵌套

结构体可以嵌套定义。

```c
struct Date {
    int year;
    int month;
    int day;
};

struct Student {
    char name[20];
    struct Date birthday;  // 嵌套结构体
    int age;
};

int main() {
    struct Student stu;
    stu.birthday.year = 2000;
    stu.birthday.month = 1;
    stu.birthday.day = 1;
    return 0;
}
```

### 14.9 位域

位域用于控制成员占用的位数。

```c
struct Flags {
    unsigned int a : 1;  // 只占1位
    unsigned int b : 2;   // 占2位
    unsigned int c : 3;   // 占3位
};
```

---

## 第十五章 文件操作

### 15.1 文件的概念

文件是存储在外部存储设备上的数据集合。C语言通过FILE结构操作文件。

```
┌─────────────────────────────────────────────────────────────┐
│                      文件操作流程                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  打开文件 ──> 读写文件 ──> 关闭文件                        │
│      │                              │                        │
│      ▼                              ▼                        │
│  FILE *fp = fopen()           fclose(fp)                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 15.2 文件打开与关闭

```c
#include <stdio.h>

int main() {
    FILE *fp;
    
    // 打开文件
    fp = fopen("test.txt", "w");  // 写入模式
    if (fp == NULL) {
        printf("文件打开失败！\n");
        return 1;
    }
    
    // 写入数据
    fprintf(fp, "Hello, World!\n");
    
    // 关闭文件
    fclose(fp);
    
    return 0;
}
```

**文件打开模式：**

| 模式 | 说明 | 文件不存在 | 文件存在 |
|------|------|-----------|-----------|
| "r" | 只读 | 报错 | 打开 |
| "w" | 只写 | 创建 | 覆盖 |
| "a" | 追加 | 创建 | 追加 |
| "r+" | 读写 | 报错 | 打开 |
| "w+" | 读写 | 创建 | 覆盖 |
| "a+" | 读写 | 创建 | 追加 |

**二进制模式：** 在上述模式后加"b"，如"rb"、"wb"、"rb+"

### 15.3 文件读写函数

| 函数 | 功能 | 说明 |
|------|------|------|
| fgetc / fputc | 读写字符 | 每次一个字符 |
| fgets / fputs | 读写字符串 | 每次一行 |
| fprintf / fscanf | 格式化读写 | 按格式读写 |
| fread / fwrite | 二进制读写 | 读写数据块 |
| feof | 判断文件结束 | 返回非0表示结束 |

### 15.4 字符读写

```c
// 写字符
fputc('A', fp);
fputc('\n', fp);

// 读字符
char ch = fgetc(fp);
while (ch != EOF) {
    putchar(ch);
    ch = fgetc(fp);
}
```

### 15.5 字符串读写

```c
// 写字符串
fputs("Hello\n", fp);
fputs("World\n", fp);

// 读字符串
char buffer[100];
while (fgets(buffer, sizeof(buffer), fp) != NULL) {
    printf("%s", buffer);
}
```

### 15.6 格式化读写

```c
// 写格式化数据
int age = 18;
float score = 95.5;
fprintf(fp, "%s %d %.1f\n", "张三", age, score);

// 读格式化数据
char name[20];
fscanf(fp, "%s %d %f", name, &age, &score);
```

### 15.7 二进制读写

```c
struct Student {
    char name[20];
    int age;
    float score;
};

struct Student stu = {"张三", 18, 95.5};

// 写入二进制
fwrite(&stu, sizeof(struct Student), 1, fp);

// 读取二进制
fread(&stu, sizeof(struct Student), 1, fp);
```

### 15.8 文件操作示例

**文件复制：**
```c
#include <stdio.h>

int main() {
    FILE *src, *dst;
    char ch;
    
    src = fopen("source.txt", "r");
    dst = fopen("dest.txt", "w");
    
    if (src == NULL || dst == NULL) {
        printf("文件打开失败！\n");
        return 1;
    }
    
    while ((ch = fgetc(src)) != EOF) {
        fputc(ch, dst);
    }
    
    fclose(src);
    fclose(dst);
    
    printf("复制完成！\n");
    return 0;
}
```

**统计文件行数：**
```c
#include <stdio.h>

int main() {
    FILE *fp;
    int lines = 0;
    char ch;
    
    fp = fopen("test.txt", "r");
    if (fp == NULL) {
        printf("文件打开失败！\n");
        return 1;
    }
    
    while ((ch = fgetc(fp)) != EOF) {
        if (ch == '\n') {
            lines++;
        }
    }
    
    fclose(fp);
    printf("文件行数: %d\n", lines);
    return 0;
}
```

---

## 第十六章 预处理

### 16.1 预处理的概念

预处理是编译前的处理阶段，主要处理以`#`开头的指令。

```
源代码(.c) → 预处理 → 预处理后的源代码(.i) → 编译 → 汇编 → 链接
```

### 16.2 宏定义

**无参宏：**
```c
#define PI 3.14159
#define MAX 100
#define TRUE 1
#define FALSE 0

int main() {
    int arr[MAX];  // 相当于 int arr[100];
    float area = PI * 5 * 5;
    return 0;
}
```

**带参宏：**
```c
#define SQR(x) ((x) * (x))
#define MAX(a, b) ((a) > (b) ? (a) : (b))
#define SWAP(a, b) { int t = a; a = b; b = t; }

int main() {
    int a = 5;
    printf("%d\n", SQR(a));  // 25
    printf("%d\n", MAX(3, 5));  // 5
    return 0;
}
```

**宏的注意事项：**
```c
// 错误示例
#define SQR(x) x * x
SQR(3 + 2);  // 相当于 3 + 2 * 3 + 2 = 11，错误！

// 正确示例
#define SQR(x) ((x) * (x))
SQR(3 + 2);  // 相当于 ((3 + 2) * (3 + 2)) = 25，正确！
```

### 16.3 条件编译

```c
#define DEBUG 1

#if DEBUG == 1
    printf("调试信息：x = %d\n", x);
#endif

#ifdef DEBUG
    printf("DEBUG已定义\n");
#endif

#ifndef MAX
    #define MAX 100
#endif

#if defined(linux)
    // Linux平台代码
#elif defined(_WIN32)
    // Windows平台代码
#else
    // 其他平台代码
#endif
```

### 16.4 文件包含

```c
// 系统头文件
#include <stdio.h>
#include <stdlib.h>

// 用户自定义头文件
#include "myheader.h"
#include "defs.h"
```

**防止重复包含：**
```c
// 方式1：使用#ifndef
#ifndef _MYHEADER_H_
#define _MYHEADER_H_

// 头文件内容

#endif

// 方式2：使用#pragma once（更简洁）
#pragma once

// 头文件内容
```

### 16.5 预定义宏

| 宏 | 说明 |
|----|------|
| `__FILE__` | 当前文件名 |
| `__LINE__` | 当前行号 |
| `__DATE__` | 编译日期 |
| `__TIME__` | 编译时间 |
| `__STDC__` | 是否符合ANSI C |

```c
printf("文件: %s\n", __FILE__);
printf("行号: %d\n", __LINE__);
printf("日期: %s\n", __DATE__);
printf("时间: %s\n", __TIME__);
```

---

## 第十七章 动态内存管理

### 17.1 内存分配函数

| 函数 | 功能 | 返回值 |
|------|------|--------|
| malloc | 分配指定字节 | 成功返回指针，失败返回NULL |
| calloc | 分配并初始化为0 | 成功返回指针，失败返回NULL |
| realloc | 重新分配 | 成功返回指针，失败返回NULL |
| free | 释放内存 | 无返回值 |

### 17.2 malloc函数

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p;
    
    // 分配10个整数的空间
    p = (int *)malloc(10 * sizeof(int));
    
    if (p == NULL) {
        printf("内存分配失败！\n");
        return 1;
    }
    
    // 使用内存
    for (int i = 0; i < 10; i++) {
        p[i] = i + 1;
    }
    
    // 释放内存
    free(p);
    p = NULL;  // 避免野指针
    
    return 0;
}
```

### 17.3 calloc函数

```c
// malloc分配（不初始化）
int *p1 = (int *)malloc(10 * sizeof(int));
// p1指向的内存是未初始化的

// calloc分配（初始化为0）
int *p2 = (int *)calloc(10, sizeof(int));
// p2指向的内存全部初始化为0
```

### 17.4 realloc函数

```c
int *p = (int *)malloc(5 * sizeof(int));

// 扩展到10个整数
p = (int *)realloc(p, 10 * sizeof(int));

// 缩减到3个整数
p = (int *)realloc(p, 3 * sizeof(int));

// 释放
free(p);
```

### 17.5 内存分配示例

**动态数组：**
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;
    printf("请输入元素个数：");
    scanf("%d", &n);
    
    // 动态分配数组
    int *arr = (int *)malloc(n * sizeof(int));
    
    if (arr == NULL) {
        printf("内存分配失败！\n");
        return 1;
    }
    
    // 输入元素
    for (int i = 0; i < n; i++) {
        printf("arr[%d] = ", i);
        scanf("%d", &arr[i]);
    }
    
    // 输出元素
    printf("数组元素：");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    // 释放内存
    free(arr);
    
    return 0;
}
```

### 17.6 常见的内存错误

| 错误 | 说明 |
|------|------|
| 内存泄漏 | 分配后未释放 |
| 野指针 | 指向已释放的内存 |
| 重复释放 | 同一块内存释放两次 |
| 越界访问 | 访问超出分配范围 |
| 空指针解引用 | 对NULL进行操作 |

**正确示例：**
```c
int *p = (int *)malloc(10 * sizeof(int));
if (p != NULL) {
    // 使用内存
    free(p);
    p = NULL;  // 释放后置为NULL
}
```

---

## 第十八章 常见错误与调试

### 18.1 语法错误

**缺少分号：**
```c
// 错误
int a = 10

// 正确
int a = 10;
```

**括号不匹配：**
```c
// 错误
if (a > b) {
    // ...
}  // 缺少一个}

// 正确
if (a > b) {
    // ...
}
```

**引号不匹配：**
```c
// 错误
char s[] = "Hello;  // 缺少右引号

// 正确
char s[] = "Hello";
```

### 18.2 逻辑错误

**= 与 == 混淆：**
```c
// 错误：赋值而非比较
if (a = 10) {  // 永远为真
    // ...
}

// 正确：比较
if (a == 10) {
    // ...
}
```

**循环边界错误：**
```c
// 错误：多循环一次
for (int i = 0; i <= n; i++) {  // 当i=n时多执行一次

}

// 正确
for (int i = 0; i < n; i++) {
    // ...
}
```

### 18.3 数组越界

```c
int arr[5];

// 错误：越界访问
for (int i = 0; i <= 5; i++) {  // i=5时越界
    arr[i] = i;
}

// 正确
for (int i = 0; i < 5; i++) {
    arr[i] = i;
}
```

### 18.4 指针错误

**空指针访问：**
```c
int *p = NULL;
*p = 10;  // 错误！对NULL解引用

// 正确
if (p != NULL) {
    *p = 10;
}
```

**野指针：**
```c
int *p;
*p = 10;  // 错误！p未初始化

// 正确
int *p = NULL;
if (p != NULL) {
    *p = 10;
}
```

### 18.5 调试方法

**使用printf调试：**
```c
int binarySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        printf("left=%d, right=%d, mid=%d\n", left, right, mid);  // 调试
        
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return -1;
}
```

**使用assert调试：**
```c
#include <assert.h>

void divide(int a, int b) {
    assert(b != 0);  // 断言b不为0
    printf("%d / %d = %d\n", a, b, a / b);
}
```

---

## 附录A 标准库函数速查

### A.1 stdio.h

| 函数 | 说明 |
|------|------|
| printf | 格式化输出 |
| scanf | 格式化输入 |
| puts | 输出字符串 |
| gets | 输入字符串（危险） |
| fgets | 安全输入字符串 |
| putchar | 输出字符 |
| getchar | 输入字符 |
| fprintf | 文件格式化输出 |
| fscanf | 文件格式化输入 |
| fopen | 打开文件 |
| fclose | 关闭文件 |
| fread | 二进制读 |
| fwrite | 二进制写 |

### A.2 stdlib.h

| 函数 | 说明 |
|------|------|
| malloc | 分配内存 |
| calloc | 分配并初始化内存 |
| realloc | 重新分配内存 |
| free | 释放内存 |
| atoi | 字符串转整数 |
| atof | 字符串转浮点数 |
| rand | 生成随机数 |
| srand | 设置随机数种子 |
| exit | 退出程序 |
| system | 执行系统命令 |

### A.3 string.h

| 函数 | 说明 |
|------|------|
| strlen | 求字符串长度 |
| strcpy | 拷贝字符串 |
| strncpy | 拷贝n个字符 |
| strcat | 连接字符串 |
| strncat | 连接n个字符 |
| strcmp | 比较字符串 |
| strncmp | 比较n个字符 |
| strchr | 查找字符 |
| strstr | 查找子串 |
| memset | 内存填充 |
| memcpy | 内存拷贝 |
| memmove | 内存移动 |

### A.4 ctype.h

| 函数 | 说明 |
|------|------|
| isdigit | 是否为数字 |
| isalpha | 是否为字母 |
| isalnum | 是否为字母或数字 |
| isspace | 是否为空格 |
| isupper | 是否为大写 |
| islower | 是否为小写 |
| toupper | 转大写 |
| tolower | 转小写 |

---

## 附录B ASCII码表

| ASCII值 | 字符 | 说明 |
|---------|------|------|
| 0-8 | 控制字符 | NUL, SOH, STX等 |
| 9 | \t | 水平制表符 |
| 10 | \n | 换行符 |
| 13 | \r | 回车符 |
| 32 | 空格 | 空格字符 |
| 48-57 | 0-9 | 数字字符 |
| 65-90 | A-Z | 大写字母 |
| 97-122 | a-z | 小写字母 |
| 127 | DEL | 删除字符 |

**完整ASCII码：**

| ASCII | 字符 | ASCII | 字符 | ASCII | 字符 | ASCII | 字符 |
|-------|------|-------|------|-------|------|-------|------|
| 0 | NUL | 32 | (空格) | 64 | @ | 96 | ` |
| 1 | SOH | 33 | ! | 65 | A | 97 | a |
| 2 | STX | 34 | " | 66 | B | 98 | b |
| 3 | ETX | 35 | # | 67 | C | 99 | c |
| 4 | EOT | 36 | $ | 68 | D | 100 | d |
| 5 | ENQ | 37 | % | 69 | E | 101 | e |
| 6 | ACK | 38 | & | 70 | F | 102 | f |
| 7 | BEL | 39 | ' | 71 | G | 103 | g |
| 8 | BS | 40 | ( | 72 | H | 104 | h |
| 9 | HT | 41 | ) | 73 | I | 105 | i |
| 10 | LF | 42 | * | 74 | J | 106 | j |
| 11 | VT | 43 | + | 75 | K | 107 | k |
| 12 | FF | 44 | , | 76 | L | 108 | l |
| 13 | CR | 45 | - | 77 | M | 109 | m |
| 14 | SO | 46 | . | 78 | N | 110 | n |
| 15 | SI | 47 | / | 79 | O | 111 | o |
| 16 | DLE | 48 | 0 | 80 | P | 112 | p |
| 17 | DC1 | 49 | 1 | 81 | Q | 113 | q |
| 18 | DC2 | 50 | 2 | 82 | R | 114 | r |
| 19 | DC3 | 51 | 3 | 83 | S | 115 | s |
| 20 | DC4 | 52 | 4 | 84 | T | 116 | t |
| 21 | NAK | 53 | 5 | 85 | U | 117 | u |
| 22 | SYN | 54 | 6 | 86 | V | 118 | v |
| 23 | ETB | 55 | 7 | 87 | W | 119 | w |
| 24 | CAN | 56 | 8 | 88 | X | 120 | x |
| 25 | EM | 57 | 9 | 89 | Y | 121 | y |
| 26 | SUB | 58 | : | 90 | Z | 122 | z |
| 27 | ESC | 59 | ; | 91 | [ | 123 | { |
| 28 | FS | 60 | < | 92 | \ | 124 | \| |
| 29 | GS | 61 | = | 93 | ] | 125 | } |
| 30 | RS | 62 | > | 94 | ^ | 126 | ~ |
| 31 | US | 63 | ? | 95 | _ | 127 | DEL |

---

**本教程基于C语言程序设计教材和菜鸟教程编写**
