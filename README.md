# libft

A custom C library that **reimplements a slice of the C standard library from scratch**, plus a set of higher-level string utilities and a linked-list toolkit. It compiles into a static archive (`libft.a`) that other C projects can link against — a personal foundation library.

## What's inside

The library is organized into three groups.

### 1 · Standard library reimplementations

Character classification, string handling, and memory operations modeled on `<ctype.h>`, `<string.h>`, and `<stdlib.h>`:

| | |
|---|---|
| **Character** | `ft_isalpha` `ft_isdigit` `ft_isalnum` `ft_isascii` `ft_isprint` `ft_toupper` `ft_tolower` |
| **Memory** | `ft_memset` `ft_bzero` `ft_memcpy` `ft_memmove` `ft_memchr` `ft_memcmp` `ft_calloc` |
| **String** | `ft_strlen` `ft_strlcpy` `ft_strlcat` `ft_strchr` `ft_strrchr` `ft_strncmp` `ft_strnstr` `ft_strdup` |
| **Conversion** | `ft_atoi` |

### 2 · Additional utilities

Higher-level helpers that aren't in the standard library:

| | |
|---|---|
| **String building** | `ft_substr` `ft_strjoin` `ft_strtrim` `ft_split` `ft_itoa` |
| **Apply-a-function** | `ft_strmapi` `ft_striteri` |
| **Output to fd** | `ft_putchar_fd` `ft_putstr_fd` `ft_putendl_fd` `ft_putnbr_fd` |

`ft_split` breaks a string into a `NULL`-terminated array on a delimiter; `ft_itoa` turns an `int` into a string (including the `INT_MIN` edge case); the `*_fd` functions write directly to any file descriptor.

### 3 · Linked list (bonus)

A singly linked list built on a simple node type:

```c
typedef struct s_list
{
    void          *content;
    struct s_list *next;
}   t_list;
```

| | |
|---|---|
| **Build** | `ft_lstnew` `ft_lstadd_front` `ft_lstadd_back` |
| **Inspect** | `ft_lstsize` `ft_lstlast` |
| **Transform / free** | `ft_lstiter` `ft_lstmap` `ft_lstdelone` `ft_lstclear` |

`ft_lstmap` applies a function to every node and returns a new list; `ft_lstiter` applies one in place; the `del`-based helpers free content safely.

## Build & use

```bash
make          # builds libft.a (standard + utility functions)
make bonus    # also includes the linked-list functions
```

Link it into your own program:

```bash
cc main.c -L. -lft -o main      # with libft.a in the current directory
```

```c
#include "libft.h"

int main(void)
{
    char **words = ft_split("hello world 42", ' ');
    /* words[0]="hello", words[1]="world", words[2]="42", words[3]=NULL */
    return (0);
}
```

## Verified

- Compiles clean with `-Wall -Wextra -Werror` (both `make` and `make bonus`).
- Edge cases checked: `ft_split` with leading/trailing/repeated delimiters, `ft_itoa(INT_MIN)`, list build/size/last operations.

---

# libft

一个**从零重写部分 C 标准库**的自制 C 库，外加一组更高层的字符串工具和一套链表工具。它编译成静态库 `libft.a`，供其他 C 项目链接使用——是一个属于自己的基础库。

## 包含内容

整个库分为三组。

### 1 · 标准库函数重写

参照 `<ctype.h>`、`<string.h>`、`<stdlib.h>` 实现的字符分类、字符串处理与内存操作：

| | |
|---|---|
| **字符** | `ft_isalpha` `ft_isdigit` `ft_isalnum` `ft_isascii` `ft_isprint` `ft_toupper` `ft_tolower` |
| **内存** | `ft_memset` `ft_bzero` `ft_memcpy` `ft_memmove` `ft_memchr` `ft_memcmp` `ft_calloc` |
| **字符串** | `ft_strlen` `ft_strlcpy` `ft_strlcat` `ft_strchr` `ft_strrchr` `ft_strncmp` `ft_strnstr` `ft_strdup` |
| **转换** | `ft_atoi` |

### 2 · 附加工具函数

标准库里没有的更高层辅助函数：

| | |
|---|---|
| **字符串构造** | `ft_substr` `ft_strjoin` `ft_strtrim` `ft_split` `ft_itoa` |
| **函数式应用** | `ft_strmapi` `ft_striteri` |
| **输出到 fd** | `ft_putchar_fd` `ft_putstr_fd` `ft_putendl_fd` `ft_putnbr_fd` |

`ft_split` 按分隔符把字符串切成以 `NULL` 结尾的数组；`ft_itoa` 把 `int` 转成字符串（含 `INT_MIN` 边界）；`*_fd` 系列直接写入任意文件描述符。

### 3 · 链表（bonus）

基于一个简单节点类型构建的单链表：

```c
typedef struct s_list
{
    void          *content;
    struct s_list *next;
}   t_list;
```

| | |
|---|---|
| **构建** | `ft_lstnew` `ft_lstadd_front` `ft_lstadd_back` |
| **查询** | `ft_lstsize` `ft_lstlast` |
| **遍历 / 释放** | `ft_lstiter` `ft_lstmap` `ft_lstdelone` `ft_lstclear` |

`ft_lstmap` 对每个节点应用函数并返回新链表；`ft_lstiter` 原地应用；带 `del` 的辅助函数可安全释放内容。

## 编译与使用

```bash
make          # 生成 libft.a（标准 + 工具函数）
make bonus    # 额外包含链表函数
```

链接进自己的程序：

```bash
cc main.c -L. -lft -o main      # libft.a 在当前目录下
```

```c
#include "libft.h"

int main(void)
{
    char **words = ft_split("hello world 42", ' ');
    /* words[0]="hello", words[1]="world", words[2]="42", words[3]=NULL */
    return (0);
}
```

## 已验证

- `-Wall -Wextra -Werror` 编译零警告（`make` 与 `make bonus` 均通过）。
- 已测边界：`ft_split` 含首尾/连续分隔符、`ft_itoa(INT_MIN)`、链表的构建/计数/取尾操作。
