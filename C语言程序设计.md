# C语言程序设计

---

## 第一章 程序与程序设计语言

### C语言的主要"单词"

#### 标识符

标识符是用来标识变量、函数、数组等实体的一种符号。标识符由字母、数字和下划线组成，且第一个字符必须是字母或下划线。

#### 关键字const

**定义**：const修饰的数据类型是指常类型，常类型的变量或对象的值是不能被更新的。

**例如**：
（1）可以定义const常量，具有不可操作性：
```c
const int Max = 100;
Max++; //会产生错误
```

（2）可以修饰指针参数，防止参数被意外修改：
```c
void f(const int i) { // 编译器就会知道i是一个常量，不允许修改
  /* code */
}
```

#### 常量

常量是有数据类型的，例如，整型常量123、实型常量12.1、字符常量'a'、字符串常量"hello world！"等。

#### 运算符

+、-、*、/、% 等。

#### 分隔符

如：`[`、`]`、`(`、`)`、`{`、`}`、`#` 都是分隔符。

### C语言主要的语法单位

- **表达式**
- **变量定义**
- **语句**
  - **表达式语句**：`i = j + 2；`
  - **分支语句**：
    ```c
    if (a > b) {
        x = a;
    } else {
        x = b;
    }
    ```
  - **循环语句**：
    ```c
    sum = 0;
    i = 1;
    while (i <= 100) {
        sum = sum + 1;
        i = i + 1;
    }
    ```
  - **复合语句**：用一对大括号{ }将若干语句顺序组合在一起就形成了一个复合语句。
  - **函数定义与调用**
  - **输入与输出**

---

## 第二章 顺序程序设计

顺序是由一句又一句的代码组成，我们自然就会知道，这些语句之间的执行是有先后的关系，如果顺序发生互换（就像前边穿衣服的顺序一样），就会产生一定的错误。

代码语句的执行在顺序程序设计的范畴内，都是由上而下的执行，因为每一个语句的执行顺序都有着前后的关联，如果随意改变执行顺序，就有可能产生错误。

### 求圆的半径以及周长的程序讲解

**代码示例**：
```c
#include <stdio.h>

void main() {
    int r = 3;
    float L;
    float S;

    L = 2 * 3.14 * r;
    S = 3.14 * r * r;

    printf("半径是%d , 的圆的周长是%f ,面积是%f \n", r, L, S);
}
```

### 代码格式

首先我们要知道的是，C语言里面有着许许多多的规则，就像人的世界一样，必须要有着约束才能正常的运作下去，因此我们写入的代码想要得到编译器的执行，就要按照C语言的约束进行代码的编写，这些约束用专业名词来说就是——语法。

#### 头文件

```c
#include <stdio.h>
```

C语言的产生目的是为了简化编程，编写C语言的人为了让我们更方便的进行代码的书写，因此有很多已经编写好的功能可以让我们直接使用（比如：求绝对值，求平方等等功能），但是由于这些功能非常多，因此C语言的编写者将这些功能进行了分类以便于我们进行使用，分好类的功能都放在一个固定的代码文件中。使用者想要使用这些功能的时候，就可以通过将这个代码文件加入到我们自己的代码中，就可以使用了。

```c
#include <需要加入的代码文件.h>    // 方法1
#include "需要加入的代码文件.h"   // 方法2
```

- **方法1** 导入代码的方法是导入C语言编写者为我们提供的功能。
- **方法2** 导入代码的方法是导入我们自己为自己提供的功能。

因为我们有的时候会在不同的地方反复使用同一个功能，如果每个地方都写一样的重复的代码，那就有点太低效率了，因此我们可以把这个功能抽出来，供所有文件一起使用。

**PS：`< >`与 `" "`导入方式的区别**

- `< >`导入方式会先去一个固定的文件夹进行寻找C语言创始人为我们写的功能。当找不到时，会再去我们自己的当前目录寻找，再找不到时就会报错。
- `" "` 这个导入方式会直接去我们当前目录进行寻找，找不到就报错。

#### 主函数

```c
void main() {
  ...代码...
}
```

代码开始执行的地方，我们所有写的代码都是要放在这个语句的大括号里边才能被编译器识别与执行，当我们没有写main的时候就会报错了，因为他找不到应该从哪里开始执行。

---

## 第三章 数据类型

### 常量与变量

- **常量**：只读，常量值不可更改。
- **变量**：程序在执行过程中变量的值可以更改。

### C语言数据类型分类

```
C语言数据类型
├── 基本类型
│   ├── 整型
│   │   ├── 基本整型 (int)
│   │   ├── 短整型 (short)
│   │   ├── 长整型 (long)
│   │   └── 双长整型 (long long)
│   ├── 字符型 (char)
│   ├── 浮点型
│   │   ├── 单精度浮点型 (float)
│   │   └── 双精度浮点型 (double)
│   └── 枚举类型 (enum)
├── 构造类型
│   ├── 数组类型 ([])
│   ├── 结构体类型 (struct)
│   └── 共用体类型 (union)
├── 指针类型 (*)
└── 空类型 (void)
```

### 数据的存储

计算机处理的所有数据都以二进制形式表示，即数据的存储和计算都采用二进制。

#### 整型数据的存储

数值可以采用原码、反码和补码等不同的方式表示。计算机内的运算，一般以补码表示数值。

| 码制 | 表示方法 | 示例 (+5 和 -5) |
|------|----------|-----------------|
| **原码** | 符号位是1，其余各位表示数值的绝对值 | +5 = 00000101<br>-5 = 10000101 |
| **反码** | 正数不变，负数符号位不变，其余各位对原码取反 | +5 = 00000101<br>-5 = 11111010 |
| **补码** | 正数不变，负数在反码基础上加1 | +5 = 00000101<br>-5 = 11111011 |

#### 实型数据的存储

实型数据采用IEEE 754标准存储，通常分为三个部分：
- **符号位** (1位)：表示正负
- **指数位** (8位)：存储指数
- **尾数位** (23位)：存储有效数字

#### 字符型数据的存储

每个字符占一个字节，用ASCII码存储。

### 基本数据类型

#### 整型与整型常量（整数）

**（1）整型**

整型是指不存在小数部分的数据类型。C语言并未规定各整型数据的长度，只要求short不长于int，long不短于int。

| 类型 | 16位系统 | 32位/64位系统 |
|------|---------|---------------|
| short | 2字节 | 2字节 |
| int | 2字节 | 4字节 |
| long | 4字节 | 4字节(32位)/8字节(64位) |
| long long | - | 8字节 |

**（2）整型常量**

即常说的整数，只要整型常量的值不超过整型数据的的取值范围，就是合法的常量。

表示方法：
- **十进制**：如 `16`
- **八进制**：如 `020`（以0开头）
- **十六进制**：如 `0x10`（以0x开头）

#### 字符型与字符常量

**（1）字符型**

可以写成字符常量的形式，还可以用相应的ASCII码表示。

例如：`char ch='A'`和`char ch=65`等价

**（2）字符型常量**

字符型常量是指单个字符，用一对单引号和其所括起来的字符表示。例如：'a'、'?'都是字符常量。

**ASCII码表**

| 字符 | ASCII码 | 字符 | ASCII码 | 字符 | ASCII码 |
|------|---------|------|---------|------|---------|
| '0' | 48 | 'A' | 65 | 'a' | 97 |
| '1' | 49 | 'B' | 66 | 'b' | 98 |
| '2' | 50 | 'C' | 67 | 'c' | 99 |
| '3' | 51 | 'D' | 68 | 'd' | 100 |
| '4' | 52 | 'E' | 69 | 'e' | 101 |
| '5' | 53 | 'F' | 70 | 'f' | 102 |
| '6' | 54 | 'G' | 71 | 'g' | 103 |
| '7' | 55 | 'H' | 72 | 'h' | 104 |
| '8' | 56 | 'I' | 73 | 'i' | 105 |
| '9' | 57 | 'J' | 74 | 'j' | 106 |
| 空格 | 32 | 'K' | 75 | 'k' | 107 |
| '+' | 43 | 'L' | 76 | 'l' | 108 |
| '-' | 45 | 'M' | 77 | 'm' | 109 |
| '*' | 42 | 'N' | 78 | 'n' | 110 |
| '/' | 47 | 'O' | 79 | 'o' | 111 |
| '=' | 61 | 'P' | 80 | 'p' | 112 |
| '(' | 40 | 'Q' | 81 | 'q' | 113 |
| ')' | 41 | 'R' | 82 | 'r' | 114 |
| '[' | 91 | 'S' | 83 | 's' | 115 |
| ']' | 93 | 'T' | 84 | 't' | 116 |
| '{' | 123 | 'U' | 85 | 'u' | 117 |
| '}' | 125 | 'V' | 86 | 'v' | 118 |
| '<' | 60 | 'W' | 87 | 'w' | 119 |
| '>' | 62 | 'X' | 88 | 'x' | 120 |
| ',' | 44 | 'Y' | 89 | 'y' | 121 |
| '.' | 46 | 'Z' | 90 | 'z' | 122 |
| ';' | 59 | '\n' | 10 | '\t' | 9 |
| ':' | 58 | '\r' | 13 | '\0' | 0 |

#### 实型与实型常量

**实型**

实型类型又称为浮点型，指存在小数的数。

| 类型 | 占用空间 | 有效数字 |
|------|---------|---------|
| float | 4字节 | 6-7位 |
| double | 8字节 | 15-16位 |
| long double | 16字节 | 18-19位 |

**实型常量**

- **小数形式**：如 `3.14`、`0.5`
- **指数形式**：如 `1.5e10`（表示1.5×10¹⁰）

### 数据的输入输出

在C语言中数据的输入输出都是通过函数的调用来实现的。

#### 整数的输入输出

| 格式符 | 含义 |
|--------|------|
| %d | 带符号十进制整数 |
| %u | 无符号十进制整数 |
| %o | 无符号八进制整数 |
| %x | 无符号十六进制整数 |
| %X | 无符号十六进制整数（大写） |

```c
int a;
scanf("%d", &a);      // 输入整数
printf("%d\n", a);    // 输出十进制
printf("%o\n", a);    // 输出八进制
printf("%x\n", a);    // 输出十六进制
```

#### 实型数据的输入输出

| 格式符 | 含义 |
|--------|------|
| %f | 单精度浮点数 |
| %lf | 双精度浮点数 |
| %.nf | 保留n位小数 |
| %e | 科学计数法 |
| %E | 科学计数法（大写E） |

```c
float f;
double d;
scanf("%f", &f);           // 输入单精度
scanf("%lf", &d);          // 输入双精度
printf("%.2f\n", f);       // 保留2位小数
printf("%e\n", d);         // 科学计数法
```

#### 字符型数据的输入输出

字符型的输入输出可以调用函数`getchar()`、`putchar()`和`scanf()`、`printf()`。

`getchar()`和`putchar`只能处理单个字符的输入输出。

```c
char a;
// 输入单个字符
a = getchar();  // 然后屏幕会停止等待你输入一个字符，用a进行存储

// 输出单个字符
char a = 'H', b = 'A';
putchar(a);
putchar(b);
// 输出：HA

// 使用scanf和printf
char ch1, ch2, ch3;
scanf("%c%c%c", &ch1, &ch2, &ch3);
printf("%c %c %c", ch1, ch2, ch3);
```

### 类型转换

#### 自动类型转换

数据混合运算时，低精度类型自动转换为高精度类型：

```
char/short → int → unsigned int → long → unsigned long → float → double
```

#### 强制类型转换

**格式**：（类型名）表达式；

```c
int i = 1;
double d = (double)i;  // 将int转换为double
```

---

## 第四章 表达式

### 算术表达式

#### 算术运算符

| 运算符 | 名称 | 示例 |
|--------|------|------|
| + | 加 | a + b |
| - | 减 | a - b |
| * | 乘 | a * b |
| / | 除 | a / b |
| % | 取余 | a % b |

#### 自增运算符和自减运算符

| 运算符 | 名称 | 说明 |
|--------|------|------|
| ++ | 自增 | 变量值加1 |
| -- | 自减 | 变量值减1 |

**注意**：
- `++a` 和 `a++` 都使a的值加1，但表达式的值不同
- `++a`：先自增，再使用值
- `a++`：先使用值，再自增

```c
int a = 5, b, c;
b = ++a;  // a=6, b=6 (先加后赋值)
c = a++;  // a=7, c=6 (先赋值后加)
```

#### 算术运算符的优先性和结合性

| 优先级 | 运算符 | 结合性 |
|--------|--------|--------|
| 高 | ++、-- | 右到左 |
| ↓ | +、-（正负） | 右到左 |
| ↓ | *、/、% | 左到右 |
| 低 | +、- | 左到右 |

**算术表达式**：用算术运算符将运算对象连接起来的符合C语言语法规则的式子成为算术表达式。

### 赋值表达式

**格式**：`变量 = 表达式；`

```c
int a, b, c;
a = 5;      // 简单赋值
b = c = a;  // 链式赋值，从右到左
```

### 复合赋值运算符

| 运算符 | 等价于 |
|--------|--------|
| += | a += b → a = a + b |
| -= | a -= b → a = a - b |
| *= | a *= b → a = a * b |
| /= | a /= b → a = a / b |
| %= | a %= b → a = a % b |

### 关系表达式

| 运算符 | 含义 |
|--------|------|
| > | 大于 |
| >= | 大于等于 |
| < | 小于 |
| <= | 小于等于 |
| == | 等于 |
| != | 不等于 |

### 逻辑表达式

| 运算符 | 名称 | 说明 |
|--------|------|------|
| && | 逻辑与 | 两边都为真才为真 |
| \|\| | 逻辑或 | 一边为真就为真 |
| ! | 逻辑非 | 取反 |

### 条件表达式

**格式**：`表达式1 ? 表达式2 : 表达式3`

```c
// 求最大值
int max = (a > b) ? a : b;
```

### 逗号表达式

**格式**：`（表达式1, 表达式2, ..., 表达式n）`

```c
int i, j;
i = 1, j = 2;  // 从左到右依次计算，整个表达式的值为最后一个表达式的值
```

### 位运算

#### 位逻辑运算符

| 运算符 | 名称 | 说明 |
|--------|------|------|
| & | 按位与 | 对应位都为1才为1 |
| \| | 按位或 | 对应位有一个为1就为1 |
| ^ | 按位异或 | 对应位相异为1 |
| ~ | 按位取反 | 0变1，1变0 |

```c
int a = 5;   // 0101
int b = 3;   // 0011
a & b = 1;   // 0001
a | b = 7;   // 0111
a ^ b = 6;   // 0110
~a = -6;     // 取反
```

#### 移位运算

| 运算符 | 名称 | 说明 |
|--------|------|------|
| << | 左移 | 二进制位左移，低位补0 |
| >> | 右移 | 二进制位右移 |

```c
int a = 5;     // 0101
a << 2;        // 010100 = 20
a >> 1;        // 0010 = 2
```

#### 特殊运算符

- **`sizeof`**：计算数据类型或变量占用的字节数
  ```c
  int a;
  sizeof(int);  // 4
  sizeof(a);    // 4
  ```

### 运算符的优先性与结合性

| 优先级 | 运算符 | 结合性 | 说明 |
|--------|--------|--------|------|
| 1 | () [] . -> | 左到右 | 最高 |
| 2 | ! ~ ++ -- + - * & sizeof | 右到左 | 单目运算符 |
| 3 | * / % | 左到右 | 乘除取余 |
| 4 | + - | 左到右 | 加减 |
| 5 | << >> | 左到右 | 移位 |
| 6 | < <= > >= | 左到右 | 关系 |
| 7 | == != | 左到右 | 相等 |
| 8 | & | 左到右 | 位与 |
| 9 | ^ | 左到右 | 位异或 |
| 10 | \| | 左到右 | 位或 |
| 11 | && | 左到右 | 逻辑与 |
| 12 | \|\| | 左到右 | 逻辑或 |
| 13 | ?: | 右到左 | 条件 |
| 14 | = += -= *= /= %= &= ^= \|= <<= >>= | 右到左 | 赋值 |
| 15 | , | 左到右 | 逗号（最低） |

---

## 第五章 分支程序设计

### if...else结构

**完整格式**：
```c
if (条件1) {
   满足条件1，于是执行这里的代码。
} else if (条件2) {
   满足条件2，于是执行这里的代码。
} else if (条件3) {
   满足条件3，于是执行这里的代码。
} else {
   以上条件均不满足，执行这里的代码。
}
```

**例如**：
```c
#include<stdio.h>

void main() {
    float score;
    printf("请输入小明的成绩，以获得相应的奖励，成绩为：");
    scanf("%f", &score);

    if (score >= 90) {
        printf("恭喜你，获得大餐一顿\n");
    } else if (score < 90 && score >= 70) {
        printf("恭喜你，获得篮球一个\n");
    } else if (score < 70 && score >= 60) {
        printf("恭喜你，获得练习册一本\n");
    } else {
        printf("恭喜你，获得大嘴巴子一个\n");
    }
}
```

### switch...case结构

**完整格式**：
```c
switch (可以得出准确值的表达式) {
   case 准确值1:
       满足准确值1时，应该执行的语句。
       break;
   case 准确值2:
       满足准确值2时，应该执行的语句。
       break;
   case 准确值3:
       满足准确值3时，应该执行的语句。
       break;
   ...
   default:
       以上都不满足，则执行这里的语句
}
```

**例如**：
```c
#include<stdio.h>

void main() {
    char score;
    printf("成绩处于 0~59之间，属于等级 D \n");
    printf("成绩处于 60~69之间，属于等级 C \n");
    printf("成绩处于 70~89之间，属于等级 B \n");
    printf("成绩处于90~100之间，属于等级 A \n");
    printf("请输入小明的成绩等级，以获得相应的奖励，等级为：");
    scanf("%c", &score);

    switch(score) {
        case 'A' : printf("恭喜你，获得大餐一顿\n");
            break;
        case 'B' : printf("恭喜你，获得篮球一个\n");
            break;
        case 'C' : printf("恭喜你，获得练习册一本\n");
            break;
        case 'D' : printf("恭喜你，获得大嘴巴子一个\n");
            break;
        default: printf("等级输入有误，程序结束！\n");
    }
}
```

### break与continue

**break**：是结束最接近break的一个流程控制语句。意思就是：当执行到break的时候，就结束掉距离break最近的一个循环或switch语句。

**例如**：
```c
#include <stdio.h>
#include <stdlib.h>

void main() {
    for (int i = 1; i <= 5; i++) {
        for (int j = 1; j <= 5; j++) {
            if (j == 3) {
                break;  // 结束内层for循环
            }
            printf(" j 的值是：%d \n", j);
        }
        printf(" *** i *** 的值是：%d \n", i);
    }
}

// 输出：
//  j 的值是：1 
//  j 的值是：2 
//  *** i *** 的值是：1 
//  j 的值是：1 
//  j 的值是：2 
//  *** i *** 的值是：2 
// ... (循环5次)
```

**continue**：是结束一个循环控制语句中的某一次。意思就是：我们循环输出的时候，其中有一次的结果我们不想输出，就可以使用continue不让他输出，但是不影响循环中的其他输出。（不像break会结束掉整个循环程序）。

**例如**：
```c
#include <stdio.h>
#include <stdlib.h>

void main() {
    for (int i = 0; i < 10; i++) {
        if (i == 3) {
            continue;  // 跳过i=3的输出
        }
        if (i == 6) {
            continue;  // 跳过i=6的输出
        }
        printf(" i 的值是：%d \n", i);
    }
    printf("循环 i 之后的内容\n");
}

// 输出：
//  i 的值是：0 
//  i 的值是：1 
//  i 的值是：2 
//  i 的值是：4 
//  i 的值是：5 
//  i 的值是：7 
//  i 的值是：8 
//  i 的值是：9 
// 循环 i 之后的内容
```

---

## 第六章 循环结构

### while

**基本结构**：
```c
while (逻辑表达式) {
   循环体；
}
```

**例如**：
```c
#include<stdio.h>

void main() {
    int num_total = 0;
    int i = 50;
    
    while (i > 0) {
        num_total = num_total + i;
        i--;
    }
    
    printf("total = %d\n", num_total);
}

// 输出：total = 1275
```

### do...while

**基本结构**：
```c
do {
   循环体；
} while (逻辑表达式);  // 先执行后判断
```

**例如**：
```c
#include<stdio.h>

void main() {
    int num_total = 0;
    int i = 50;
    
    do {
        num_total = num_total + i;
        i--;
    } while (i > 0);
    
    printf("total = %d\n", num_total);
}

// 输出：total = 1275
```

### for

**基本结构**：
```c
for (循环变量赋初始值; 循环次数的控制条件; 循环变量改变值) {
   循环体;
}
```

**例1**：
```c
#include<stdio.h>

void main() {
    int total = 0;
    
    for (int i = 1; i <= 50; i++) {
        total = total + i;
    }  //循环结束后i变量消失
    
    printf("1~50所有整数和为：%d\n", total);
}

// 输出：1~50所有整数和为：1275
```

**例2**：
```c
int i = 1;
for (; i <= 10; i++) {
   循环体;
}  // 循环结束后i值改变，i=11
```

**例3**：
```c
int i = 1;
for (; i <= 50;) {
    total = total + i;
    i++;  // 我们把增量写在循环体最后了
}
```

### 三种循环对比

| 循环类型 | 特点 | 使用场景 |
|----------|------|----------|
| while | 先判断后执行 | 循环次数不确定 |
| do...while | 先执行后判断 | 至少执行一次 |
| for | 最灵活 | 循环次数确定 |

---

## 第七章 数组

### 一维数组定义

**格式**：`类型名 数组名[数组长度]；`

**例如**：
```c
int A[3] = {1, 2, 3};      // 指定长度并初始化
int B[] = {1, 2, 3, 4};    // 自动计算长度，长度为4
```

### 二维数组定义

**格式**：`类型名 数组名[行数][列数]；`

**例如**：
```c
int A[2][3] = {{1, 2, 3}, {4, 5, 6}};
```

**二维数组在内存中的存储**：按行存储，先存第一行，再存第二行...

```
内存地址:  0x00  0x01  0x02  0x03  0x04  0x05
数据:      1     2     3     4     5     6
          ←──── 第一行 ────→  ←──── 第二行 ────→
```

**错误定义**：
```c
int A[][] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};      // 错误：行列都省略
int A[3][] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};      // 错误：列数不可省略
```

**正确定义**：
```c
int A[][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};      // 正确：可省略行数
int A[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};    // 正确：行列都指定
```

### 字符数组

```c
char a = 'J';                           // 单个字符定义
char b[4] = {'L', 'O', 'V', 'E'};     // 字符数组定义
char c[] = {'I', ' ', 'L', 'O', 'V', 'E', ' ', 'C', 'H', 'I', 'N', 'A'};
```

### 字符串

```c
char str[50] = {"I LOVE CHINA"};
// 或者
char str[50] = "I LOVE CHINA";
```

**重要概念**：C语言引入了一种机制，在字符串实际内容的结尾处会默认加上一个字符串结束符`'\0'`，当编译器读取一个字符串的时候读取到`'\0'`的时候就认为字符串结束了。并且，`'\0'`不算入字符串的长度之内。

**字符串存储示意**：
```
字符:  I   空格  L   O   V   E   空格  C   H   I   N   A   \0
下标:  0   1     2   3   4   5   6     7   8   9   10  11  12
```

**字符串输入**：
```c
char str[50];
int i = 0;
// 方法1：使用getchar
while ((str[i] = getchar()) != '\n') {
    i++;
}
str[i] = '\0';

// 方法2：使用scanf
scanf("%s", str);  // 遇到空格或换行停止

// 方法3：使用gets（不安全，不推荐）
gets(str);
```

**字符串输出**：
```c
printf("%s", str);  // 使用格式符%s
puts(str);          // 使用puts函数，自动换行
```

---

## 第八章 指针

### 指针与指针变量

- **指针**：是一个具体的数据，这个数据就是地址。
- **指针变量**：是一个变量，用来存放数据（存放指针）。

### 指针变量定义

**格式**：`类型名 *指针变量名；`

**注意**：指针变量的数据类型与其定义之时前边的数据类型无关，指针变量的数据类型恒为**地址类型**（本质上都是存储地址的整数）。

**例如**：
```c
int *p;      //定义一个指针变量p，指向整型变量
char *cp;    //定义一个指针变量cp，指向字符型变量
float *fp;   //定义一个指针变量fp，指向浮点型变量
double *dp;  //定义一个指针变量dp，指向双精度实型变量
```

### 指针变量赋值

```c
int a = 10;
int *p;

p = &a;       // p指向a的地址
p = 0;        // 空指针，不指向任何单元
p = NULL;     // 空指针，等价于0
p = (int *)1234;  // 强制类型转换，指向地址1234
```

### 指针变量的运算

#### 取地址运算和间接访问运算

单目运算符`&`用于给出变量的地址：
```c
int *p, a = 23;
p = &a;       // p指向a的地址，指针的类型和它所指向变量的类型必须相同

int b;
b = *p;       // b = a = 23，通过指针访问变量
```

#### 指针算术运算

```c
int *p, a[100];
p = a;       // p指向数组首元素

p = a + 1;   // 指向a[1]，指针每次加1或减1，
             // 不是指针的值加1或减1，
             // 而是加上或减去该指针所指向那个变量数据类型的长度
p = &a[1];   // 与上面等价
```

### 指针作为函数的参数

**例**：输入年份和天数，输出对应的年、月、日。要求定义和调用函数`month_day(int year, int yearday, int *pmonth, int *pday)`，其中year是年，yearday是天数，pmonth和pday指向的变量保存计算得出的月和日。

```c
#include<stdio.h>

void month_day(int year, int yearday, int* pmonth, int* pday);

int main(void) {
    int day, month, year, yearday;
    printf("input year and yearday:");
    scanf("%d%d", &year, &yearday);
    month_day(year, yearday, &month, &day);
    printf("%d-%d-%d\n", year, month, day);	
    return 0;
}

void month_day(int year, int yearday, int* pmonth, int* pday) {
    int k, leap;
    int tab[2][13] = {
        {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31},
        {0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31},
    };  //存放非闰年和闰年每个月的天数

    leap = (year % 4 == 0 && year % 100 != 0) || year % 400 == 0;
    for (k = 1; yearday > tab[leap][k]; k++)
        yearday -= tab[leap][k];
    *pmonth = k;
    *pday = yearday;
}

// input year and yearday:2024 330
// 2024-11-25
```

### 指针、数组和地址的关系

```c
int *p, a[100];  //a为指针常量，p为指针变量
```

**等价语句**：
```c
p = a;      // a为数组名，指针常量
p = &a[0];  // 与上面等价，都是指向首元素
```

**等价语句**：
```c
p = a + 1;  // 指针每次加1或减1
p = &a[1];  // 与上面等价
```

### 数组名作为函数的参数

```c
#include<stdio.h>

void printArray(int arr[], int n);  // arr实际上是指针

int main() {
    int a[] = {1, 2, 3, 4, 5};
    printArray(a, 5);
    return 0;
}

void printArray(int arr[], int n) {  // 等价于 int *arr
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
}
```

### 字符串和字符指针

#### 字符串常量的存储

字符串是用一对双引号括起来的字符序列，字符常量在内存中的存储位置由系统自动安排，字符常量中的所有字符在内存中连续存放。

系统在存储字符常量时先给定一个起始地址，从该起始地址开始连续存放字符串中的字符，该起始地址就是字符串常量的值。也就是说，**字符串常量实质上是一个指向该字符串首字符的指针常量**。

```c
char *p = "hello";  // p指向字符串"hello"的首字符'h'
```

#### 字符数组与字符指针的区别

| 特性 | 字符数组 | 字符指针 |
|------|----------|----------|
| 内存 | 分配在栈上 | 指向常量区的字符串 |
| 修改 | 可以修改字符 | 不能修改（未定义行为） |
| 赋值 | 定义时初始化 | 可以后期指向其他字符串 |
| 空间 | 固定大小 | 只存储地址 |

```c
// 字符数组
char str1[] = "hello";
str1[0] = 'H';  // 正确，可以修改

// 字符指针
char *str2 = "hello";
str2[0] = 'H';  // 危险！可能崩溃，字符串常量不可修改
```

### 常用的字符串处理函数

头文件`stdio.h`和`string.h`给出了字符串处理函数的原型。

| 函数 | 功能 | 所在头文件 |
|------|------|-----------|
| `gets(s)` | 输入字符串 | stdio.h |
| `puts(s)` | 输出字符串 | stdio.h |
| `strlen(s)` | 求字符串长度 | string.h |
| `strcpy(s1, s2)` | 复制字符串 | string.h |
| `strcat(s1, s2)` | 连接字符串 | string.h |
| `strcmp(s1, s2)` | 比较字符串 | string.h |

```c
#include <string.h>

char s1[20] = "hello";
char s2[] = "world";

// 复制
strcpy(s1, "hi");        // s1 = "hi"

// 连接
strcat(s1, s2);          // s1 = "hiworld"

// 比较
int result = strcmp(s1, s2);  // result < 0 (s1 < s2)

// 长度
int len = strlen(s1);    // len = 7
```

### 用指针实现动态内存分配

#### 动态内存分配函数

| 函数 | 说明 | 函数原型 |
|------|------|----------|
| `malloc()` | 分配指定字节 | `void *malloc(size_t size);` |
| `calloc()` | 分配并初始化为0 | `void *calloc(size_t n, size_t size);` |
| `realloc()` | 重新分配 | `void *realloc(void *ptr, size_t size);` |
| `free()` | 释放内存 | `void free(void *ptr);` |

```c
#include <stdlib.h>

// 分配10个int的空间
int *p = (int *)malloc(sizeof(int) * 10);

// 分配并初始化为0
int *q = (int *)calloc(10, sizeof(int));

// 重新分配
p = (int *)realloc(p, sizeof(int) * 20);

// 释放
free(p);
free(q);
```

---

## 第九章 函数

### 函数的定义

**函数的一般形式**：
```c
函数类型 函数名(形式参数表)  //函数首部
{
    函数实现过程  //函数体
}
```

**例如**：
```c
int max(int a, int b) {
    return a > b ? a : b;
}
```

### 函数的调用

#### 函数调用的过程

1. 为主调函数分配调用栈帧
2. 为被调函数分配新的栈帧
3. 传递参数（值传递）
4. 执行被调函数
5. 返回结果到主调函数
6. 释放栈帧

#### 函数调用的形式

```c
// 作为表达式语句
printf("hello");

// 作为表达式
result = max(a, b);

// 作为另一个函数的参数
printf("%d", max(a, b));
```

#### 参数传递

**值传递**：将实参的值复制一份传递给形参，形参的改变不会影响实参。

```c
void swap(int x, int y) {
    int temp = x;
    x = y;
    y = temp;
}
// 调用
int a = 1, b = 2;
swap(a, b);  // a和b的值不变！
```

**地址传递**：传递地址，形参通过地址访问实参，可以改变实参的值。

```c
void swap(int *x, int *y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}
// 调用
int a = 1, b = 2;
swap(&a, &b);  // a和b的值交换了！
```

#### 函数结果返回

```c
int add(int a, int b) {
    return a + b;  // 返回整型值
}

void print() {
    return;  // 无返回值的函数可以单独使用return
}
```

### 函数原型声明

**格式**：`返回类型 函数名(参数类型列表);`

```c
#include<stdio.h>

void month_day(int year, int yearday, int* pmonth, int* pday);  //声明计算月、日的函数
int sum(int* p, int n);  //计算数组和

int main(void) {
    int a, b[100], *p = NULL;
    a = 1;
    for (int i = 0; i < 100; i++) {
        b[i] = i;
    }
    printf("%d", sum(b, 10));
    char a[] = "hello world!";
    puts(a);
    return 0;
}

void month_day(int year, int yearday, int* pmonth, int* pday) {
    int k, leap;
    int tab[2][13] = {
        {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31},
        {0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31},
    };
    leap = (year % 4 == 0 && year % 100 != 0) || year % 400 == 0;
    for (k = 1; yearday > tab[leap][k]; k++)
        yearday -= tab[leap][k];
    *pmonth = k;
    *pday = yearday;
}

int sum(int *p, int n) {
    int i, s = 0;
    for (i = 0; i < n; i++) {
        s += *(p + i);
    }
    return s;
}
```

### 不返回结果的函数

```c
void printHello() {
    printf("Hello!\n");
    return;  // 可省略
}
```

### 局部变量和全局变量

#### 局部变量

局部变量都定义在函数的内部，有效使用范围局限于所在的函数内。

```c
void func() {
    int a = 10;  // 局部变量
    // a只能在这个函数内使用
}

int main() {
    // printf("%d", a);  // 错误！a不在这里
    return 0;
}
```

#### 全局变量

定义在函数外而不属于任何函数的变量称为全局变量。全局变量的作用范围是从定义开始到程序所在文件的结束，它对作用范围内的所有函数都起作用。

```c
int global = 100;  // 全局变量

void func1() {
    printf("%d", global);  // 可以访问
}

void func2() {
    global = 200;  // 可以修改
}
```

### 变量的生存周期和静态局部变量

#### 变量的生存周期

| 存储类别 | 生命周期 | 作用域 | 存储位置 |
|----------|----------|--------|----------|
| 自动变量 | 函数结束 | 函数内 | 栈 |
| 静态变量 | 程序结束 | 函数内 | 静态区 |
| 寄存器变量 | 函数结束 | 函数内 | 寄存器 |
| 全局变量 | 程序结束 | 文件内 | 静态区 |

#### 变量存储的内存分布

```
┌─────────────────┐ 高地址
│     代码区       │ 存放程序代码
├─────────────────┤
│     全局区       │ 存放全局变量和静态变量
├─────────────────┤
│     堆区         │ 动态分配 (malloc/free)
├─────────────────┤
│     栈区         │ 函数调用、局部变量
└─────────────────┘ 低地址
```

#### 静态变量

**静态局部变量**：使用`static`关键字，在函数内部定义，但整个程序运行期间一直存在。

```c
void counter() {
    static int count = 0;  // 第一次调用时初始化，之后保留值
    count++;
    printf("count = %d\n", count);
}

int main() {
    counter();  // count = 1
    counter();  // count = 2
    counter();  // count = 3
    return 0;
}
```

---

## 第十章 结构体

### 结构概念与定义

结构体是用户构造的数据类型，可以把不同类型的数据组合成一个整体。

**定义格式**：
```c
struct 结构体名 {
    成员类型 成员名1;
    成员类型 成员名2;
    ...
};
```

**例如**：
```c
struct Student {
    char name[20];
    int age;
    float score;
};
```

### typedef语句定义

使用`typedef`为结构体起别名，简化使用：

```c
typedef struct Student {
    char name[20];
    int age;
    float score;
} Student;
// 之后可以直接用Student定义变量
```

### 结构的嵌套定义

结构体可以嵌套定义：

```c
struct Date {
    int year;
    int month;
    int day;
};

struct Student {
    char name[20];
    struct Date birthday;  // 嵌套结构体
};
```

### 结构体变量的定义和初始化

#### 单独定义

```c
struct Student {
    char name[20];
    int age;
    float score;
};

int main() {
    struct Student stu1;           // 定义结构体变量
    struct Student stu2 = {"Tom", 18, 90.5};  // 初始化
    return 0;
}
```

#### 在main主函数中定义

```c
int main() {
    struct Student {
        char name[20];
        int age;
    } stu;  // 定义时直接创建变量
    
    return 0;
}
```

#### 混合定义

```c
struct Student {
    char name[20];
    int age;
} stu1, stu2;  // 定义类型的同时定义变量
```

#### 初始化

```c
struct Student stu = {"Tom", 18, 90.5};           // 顺序初始化
struct Student stu = {.name = "Tom", .age = 18};  // 指定成员初始化(C99)
```

### 结构体变量的使用

```c
struct Student {
    char name[20];
    int age;
    float score;
};

int main() {
    struct Student stu;
    
    // 使用点运算符访问成员
    strcpy(stu.name, "Tom");
    stu.age = 18;
    stu.score = 90.5;
    
    printf("%s %d %.1f\n", stu.name, stu.age, stu.score);
    return 0;
}
```

### 结构体数组

```c
struct Student {
    char name[20];
    int age;
    float score;
};

int main() {
    struct Student stus[3] = {
        {"Tom", 18, 90.5},
        {"Jerry", 19, 88.0},
        {"Mike", 20, 95.5}
    };
    
    for (int i = 0; i < 3; i++) {
        printf("%s %d %.1f\n", stus[i].name, stus[i].age, stus[i].score);
    }
    return 0;
}
```

### 结构体指针

```c
struct Student {
    char name[20];
    int age;
};

int main() {
    struct Student stu = {"Tom", 18};
    struct Student *p = &stu;
    
    // 两种方式访问成员
    printf("%s %d\n", (*p).name, (*p).age);  // 方式1
    printf("%s %d\n", p->name, p->age);     // 方式2：更常用
    return 0;
}
```

### 结构体指针作为函数的参数

```c
struct Student {
    char name[20];
    int age;
};

void printStudent(struct Student *p) {
    printf("%s %d\n", p->name, p->age);
}

int main() {
    struct Student stu = {"Tom", 18};
    printStudent(&stu);
    return 0;
}
```

---

## 第十一章 函数与程序结构

### 递归程序设计

递归：函数调用自身

**递归的两个要素**：
1. 递归出口（终止条件）
2. 递归公式（规模缩小）

#### 汉诺塔问题

**问题描述**：有三根柱子A、B、C，A柱上有n个盘子（从上到下编号1~n，大的在下面），要求将所有盘子从A移动到C，移动规则：
1. 每次只能移动一个盘子
2. 大盘子不能放在小盘子上面

```c
void hanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", from, to);
        return;
    }
    hanoi(n - 1, from, aux, to);        // 将n-1个盘子从A移到B
    printf("Move disk %d from %c to %c\n", n, from, to);  // 移动第n个
    hanoi(n - 1, aux, to, from);       // 将n-1个盘子从B移到C
}

int main() {
    hanoi(3, 'A', 'C', 'B');
    return 0;
}

// 输出：
// Move disk 1 from A to C
// Move disk 2 from A to B
// Move disk 1 from C to B
// Move disk 3 from A to C
// Move disk 1 from B to A
// Move disk 2 from B to C
// Move disk 1 from A to C
```

#### 用递归求N的阶乘

```c
int factorial(int n) {
    if (n <= 1) return 1;  // 递归出口
    return n * factorial(n - 1);  // 递归公式
}

int main() {
    printf("%d\n", factorial(5));  // 120
    return 0;
}
```

#### 求M和N的最大公约数（辗转相除法）

```c
int gcd(int m, int n) {
    if (n == 0) return m;  // 递归出口
    return gcd(n, m % n);  // 递归公式
}

int main() {
    printf("%d\n", gcd(24, 18));  // 6
    return 0;
}
```

#### 将整数N逆序输出

```c
void reverse(int n) {
    if (n < 10) {
        printf("%d", n);
        return;
    }
    printf("%d", n % 10);
    reverse(n / 10);
}

int main() {
    reverse(12345);  // 54321
    return 0;
}
```

#### 分治法求解金块问题

**问题**：有一堆金块，最重的金块重量是其他金块的两倍，找出最重的金块。

### 宏基本定义

**定义**：`#define 宏名 替换文本`

```c
#define PI 3.14159
#define MAX 100

int main() {
    printf("%.2f\n", PI);      // 3.14
    int arr[MAX];              // 编译时替换为 int arr[100];
    return 0;
}
```

### 带参数的宏定义

**定义**：`#define 宏名(参数) 替换文本`

```c
#define SQR(x) ((x) * (x))
#define MAX(a, b) ((a) > (b) ? (a) : (b))

int main() {
    printf("%d\n", SQR(5));       // 25
    printf("%d\n", MAX(3, 4));    // 4
    return 0;
}
```

**注意**：宏参数要加括号，防止副作用。

```c
#define SQR(x) x * x  // 错误！
// SQR(3 + 2) 会变成 3 + 2 * 3 + 2 = 11

#define SQR(x) ((x) * (x))  // 正确
// SQR(3 + 2) 会变成 ((3 + 2) * (3 + 2)) = 25
```

### 文件包含

```c
#include "myheader.h"   // 用户自定义头文件
#include <stdio.h>      // 系统头文件
```

### 编译预处理

#### 条件编译#if

```c
#define DEBUG 1

#if DEBUG == 1
    printf("Debug mode\n");
#else
    printf("Release mode\n");
#endif
```

#### #ifdef和#ifndef

```c
#define DEBUG

#ifdef DEBUG
    // 如果定义了DEBUG，执行这里
#endif

#ifndef HEADER_H
#define HEADER_H
    // 如果没有定义HEADER_H，执行这里
    // 常用于头文件保护
#endif
```

### 文件模块的通信

#### 多文件模块的学生信息系统

通常一个项目分为多个源文件：
- `main.c`：主函数
- `student.h`：声明
- `student.c`：实现

#### 外部变量

使用`extern`声明在其他文件中定义的全局变量：

```c
// file1.c
int global_var = 100;

// file2.c
extern int global_var;  // 声明外部变量
printf("%d\n", global_var);
```

#### 静态全局变量

使用`static`修饰全局变量，限制其作用域为本文件：

```c
// file.c
static int internal_var = 10;  // 只能在本文件使用
```

### 函数与程序文件模块

将函数声明和定义分离，提高代码可维护性：

```c
// student.h
typedef struct {
    char name[20];
    int age;
} Student;

void printStudent(Student *p);

// student.c
#include "student.h"

void printStudent(Student *p) {
    printf("%s %d\n", p->name, p->age);
}

// main.c
#include "student.h"

int main() {
    Student stu = {"Tom", 18};
    printStudent(&stu);
    return 0;
}
```

---

## 第十二章 指针进阶

### 指针数组

指针数组是数组，每个元素都是指针：

```c
int a = 1, b = 2, c = 3;
int *p[3] = {&a, &b, &c};  // 指针数组

printf("%d\n", *p[0]);  // 1
printf("%d\n", *p[1]);  // 2
```

### 指向指针的指针

指向指针的指针，即二级指针：

```c
int a = 10;
int *p = &a;      // p是指向a的指针（一级指针）
int **pp = &p;     // pp是指向p的指针（二级指针）

printf("%d\n", *p);    // 10
printf("%d\n", **pp);  // 10
```

#### 用指针数组处理多个字符串

```c
char *names[] = {"Tom", "Jerry", "Mike", "John"};

for (int i = 0; i < 4; i++) {
    printf("%s\n", names[i]);
}
```

#### 指针数组与二维数组

```c
// 二维数组
char str1[][20] = {"hello", "world"};

// 指针数组（更灵活）
char *str2[] = {"hello", "world"};
```

| 对比 | 二维数组 | 指针数组 |
|------|----------|----------|
| 内存 | 连续 | 不一定连续 |
| 大小 | 固定 | 可以动态分配 |
| 赋值 | 不可直接赋值字符串 | 可以指向新字符串 |

#### 动态输入多个字符串

```c
char *names[5];

for (int i = 0; i < 5; i++) {
    names[i] = (char *)malloc(100 * sizeof(char));
    scanf("%s", names[i]);
}

// 使用完后释放
for (int i = 0; i < 5; i++) {
    free(names[i]);
}
```

#### 字符定位

```c
char *strchr(const char *s, int c);  // 查找字符c首次出现的位置
char *strstr(const char *s1, const char *s2);  // 查找子串s2首次出现的位置
```

```c
char str[] = "hello world";
char *p = strchr(str, 'o');  // 指向第一个'o'
if (p) printf("Found at %ld\n", p - str);  // Found at 4

p = strstr(str, "world");  // 指向"world"
if (p) printf("Found at %ld\n", p - str);  // Found at 6
```

### 指针作为函数的返回值

指针函数：返回指针的函数

```c
char *strcopy(char *dest, const char *src) {
    char *p = dest;
    while (*src != '\0') {
        *dest = *src;
        dest++;
        src++;
    }
    *dest = '\0';
    return p;  // 返回目标字符串首地址
}
```

**注意**：不要返回指向局部变量的指针！

```c
char *bad_function() {
    char local[] = "hello";  // 局部变量，函数结束后销毁
    return local;  // 危险！返回后内存已释放
}
```

### 指向函数的指针

函数也有地址，可以定义指向函数的指针。

#### 指针函数的定义

```c
返回类型 (*指针变量名)(参数类型列表);
```

```c
int (*p)(int, int);  // p是指向返回int、两个int参数的函数的指针
```

#### 通过函数指针调用函数

```c
int add(int a, int b) {
    return a + b;
}

int main() {
    int (*p)(int, int) = add;  // p指向add函数
    int result = (*p)(1, 2);   // 通过指针调用
    // 或者
    result = p(1, 2);          // 直接调用
    printf("%d\n", result);    // 3
    return 0;
}
```

#### 函数指针作为函数的参数（回调函数）

```c
void visit(int *arr, int n, void (*func)(int)) {
    for (int i = 0; i < n; i++) {
        func(arr[i]);  // 调用传入的函数
    }
}

void print(int x) {
    printf("%d ", x);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    visit(arr, 5, print);  // 1 2 3 4 5
    return 0;
}
```

**常见应用**：qsort函数的比较函数

```c
int compare(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);  // 升序
}

int main() {
    int arr[] = {3, 1, 4, 1, 5, 9, 2, 6};
    qsort(arr, 8, sizeof(int), compare);
    for (int i = 0; i < 8; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```
