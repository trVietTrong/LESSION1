# Advance_C_Cpp

## Contents

<details>
<summary>LESSON 1: COMPILER - MACRO</summary>

---

## I. COMPILER

### 1. Định Nghĩa

#### 1.1 Quá Trình Biên Dịch
Quá trình biên dịch là quá trình chuyển đổi từ ngôn ngữ bậc cao (C/C++, Pascal, Java, C#...) sang ngôn ngữ đích (ngôn ngữ máy) để máy tính có thể hiểu và thực thi.

#### Quá trình biên dịch gồm 4 giai đoạn:

1. **Giai đoạn tiền xử lý (Pre-processor)**
2. **Giai đoạn dịch NNBC sang Assembly (Compiler)**
3. **Giai đoạn dịch Assembly sang ngôn ngữ máy (Assembler)**
4. **Giai đoạn liên kết (Linker)**

![Quá trình biên dịch](compiler1.jpg)

### 1.2 Hoạt Động

#### 1. Giai đoạn tiền xử lý - Preprocessor
- Nhận mã nguồn.
- Xóa bỏ chú thích, comments của chương trình.
- Xử lý các chỉ thị tiền xử lý (bắt đầu bằng dấu `#`).
- Gộp các file `.c`, `.h`... thành một file `.i`.
- Giữ lại các biến và hàm.
- **Lệnh:** `gcc -E main.c -o main.i`

Ví dụ:  
![Quá trình tiền xử lý](pre.jpg)

Giải thích: Nội dung của thư viện `stdio.h` và file `Test.c` sẽ được copy vào file `Test1.i`. Các macro định nghĩa sẽ được thay thế và giữ lại các biến và hàm.

#### 2. Compiler (Giai đoạn dịch NNBC sang Assembly)
- Biên dịch file `.i` thành file ngôn ngữ Assembly `.s`.
- **Lệnh:** `gcc -S main.i -o main.s`

#### 3. Assembler (Giai đoạn dịch Assembly sang ngôn ngữ máy)
- Biên dịch ngôn ngữ Assembly thành ngôn ngữ máy (0 và 1). Tạo ra tệp tin Object `.o`.
- **Lệnh:** `gcc -c main.s -o main.o`

#### 4. Linker (Giai đoạn liên kết)
- Một hoặc nhiều file `.o` sẽ được liên kết thành một file thực thi `.exe`.
- **Lệnh:** `gcc main.o -o filename`

---

## II. MACRO

### 1. Định Nghĩa

Trong ngôn ngữ lập trình C, macro là một cách để định nghĩa một khối mã nguồn có thể được sử dụng nhiều lần trong chương trình. Macro được xác định bằng chỉ thị `#define`. Khi chương trình được biên dịch, macro sẽ được thay thế bằng nội dung mà nó định nghĩa trước khi mã nguồn được biên dịch.

Macro trong C gồm:
1. Chỉ thị bao hàm tệp
2. Chỉ thị định nghĩa macro
3. Chỉ thị biên dịch có điều kiện

### 1.1 Chỉ Thị Bao Hàm Tệp

- **Sử dụng `#include <header.h>`**: Trình biên dịch tìm kiếm tệp header trong các thư mục chuẩn của hệ thống.
  - Ví dụ: `#include <stdio.h>`, `#include <math.h>`

- **Sử dụng `#include "header.h"`**: Trình biên dịch tìm tệp header trong cùng thư mục với file mã nguồn trước khi tìm trong các thư mục khác.
  - Ví dụ: `#include "myheader.h"`

### 1.2 Chỉ Thị Định Nghĩa Macro

- Định nghĩa hằng số, chuỗi, hoặc hàm.

```c
#include <stdio.h>
#include "Test2.c"

#define PI 3.14
#define SIZE 20
#define CHUOI "Hello World"

#define FUNC(name, cmd) \
void name() { \
    printf(cmd); \
}

FUNC(Test11, "My name is Trong");
```

- Định nghĩa các hằng số `PI`, `SIZE`, và chuỗi `CHUOI` sử dụng `#define`.
- Sử dụng macro `FUNC` để định nghĩa một hàm với tên và nội dung truyền vào.

### 1.3 Chỉ Thị Hủy Định Nghĩa Macro

```c
#include <stdio.h>

#define PI 3.14159

int main() {
    printf("Value of PI: %f\n", PI);

    #undef PI
    #define PI 55
    printf("Value of PI after undef: %f\n", PI);

    return 0;
}
```

### 1.4 Chỉ Thị Biên Dịch Có Điều Kiện

- **`#ifdef` và `#ifndef`**: Kiểm tra xem một macro đã được định nghĩa hay chưa.

```c
#include <stdio.h>

#define PI 3.14

int main() {
    #ifdef PI
        printf("PI = 3.14\n");
    #endif

    return 0;
}
```

- **`#if`, `#elif`, `#else`, `#endif`**: Biên dịch dựa trên giá trị của các biểu thức.

```c
#include <stdio.h>

#define ESP32 1
#define STM32 2
#define ATmega 3

#define MCU STM32

int main() {
    #if MCU == STM32
        printf("STM32\n");
    #elif MCU == ESP32
        printf("ESP32\n");
    #elif MCU == ATmega
        printf("ATmega\n");
    #else
        printf("Unknown MCU\n");
    #endif

    return 0;
}
```

### 1.5 Variadic Macro

- Variadic macros cho phép định nghĩa macro với số lượng tham số biến đổi.

```c
#include <stdio.h>

#define NUMBER(...) printf(__VA_ARGS__)

int main() {
    NUMBER("Value of x: %d, y: %f\n", 10, 3.14);
    return 0;
}
```

---
