---
title: 最佳做法和示例 (SAL)
ms.date: 11/04/2016
ms.topic: conceptual
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 27570e282c230d4bec47e70aa1bcdd053b75597c
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236747"
---
# <a name="best-practices-and-examples-sal"></a>最佳做法和示例 (SAL)
下面是一些关于充分利用源代码批注语言 (SAL)，并避免一些常见问题的方法。

## <a name="_in_"></a>\_In\_

如果函数应写入元素，请使用 `_Inout_` 而不是 `_In_`。 这在从旧的宏自动转换为 SAL 的情况下尤为重要。 在 SAL 之前，许多程序员使用宏作为注释，这些宏命名为 `IN`、`OUT`、`IN_OUT`，或是这些宏的变体。 尽管建议您将这些宏转换为 SAL，但在转换时应谨慎，因为代码自写入原型以来可能已经发生改变，并且旧的宏可能已不再反映代码的作用。 请特别注意 `OPTIONAL` 注释宏，因为它经常错误放置；例如，在逗号错误的一边。

```cpp

// Incorrect
void Func1(_In_ int *p1)
{
    if (p1 == NULL)
        return;

    *p1 = 1;
}

// Correct
void Func2(_Inout_ PCHAR p1)
{
    if (p1 == NULL)
        return;

    *p1 = 1;
}
```

## <a name="_opt_"></a>\_opt\_

如果不允许调用方传递 null 指针，请使用 `_In_` 或 `_Out_`，而不是 `_In_opt_` 或 `_Out_opt_`。 这甚至适用于函数，该函数会检查其参数，如果参数不应为 NULL 但却为 NULL，则会返回错误。 尽管让函数检查其参数中是否存在意外的 NULL 并正常返回是一种很好的防御性编码做法，但并不意味着参数批注可以是可选`_*Xxx*_opt_`类型（）。

```cpp

// Incorrect
void Func1(_Out_opt_ int *p1)
{
    *p = 1;
}

// Correct
void Func2(_Out_ int *p1)
{
    *p = 1;
}
```

## <a name="_pre_defensive_-and-_post_defensive_"></a>\_预先\_ \_防御\_和防御后\_的防御\_

如果函数出现在信任边界上，则建议您使用 `_Pre_defensive_` 批注。  “防御性”修饰符可修改特定批注，用于指明在调用时应严格检查界面，但在实现体中，应假定可能会传递错误的参数。 这种情况下，在信任边界上将首选 `_In_ _Pre_defensive_`，以便指明尽管调用方在尝试传递 NULL 时会出现错误，但还是会分析函数体（就像参数可能是 NULL 一样），因此，任何取消指针引用而不首先检查其是否为 NULL 的尝试都会被标记。  还可使用 `_Post_defensive_` 批注，以便用于回调，其中假设受信任方为调用方，而不受信任的代码为调用的代码。

## <a name="_out_writes_"></a>\_Out\_写入\_

下面的示例演示一种常见的 `_Out_writes_` 误用案例。

```cpp

// Incorrect
void Func1(_Out_writes_(size) CHAR *pb,
    DWORD size
);
```

批注 `_Out_writes_` 表示您具有缓冲区。 它分配了 `cb` 个字节，其中第一个字节在退出时进行初始化。 此批注严格来说并没有错误，并且有助于表示分配的大小。 但是，它并未说明函数初始化了多少元素。

下一个示例演示三种完全指定缓冲区初始化部分的确切大小的正确方法。

```cpp

// Correct
void Func1(_Out_writes_to_(size, *pCount) CHAR *pb,
    DWORD size,
    PDWORD pCount
);

void Func2(_Out_writes_all_(size) CHAR *pb,
    DWORD size
);

void Func3(_Out_writes_(size) PSTR pb,
    DWORD size
);
```

## <a name="_out_-pstr"></a>\_Out\_ PSTR

任何时候，使用 `_Out_ PSTR` 几乎都是错误的。 这可解释为具有指向字符缓冲区的输出参数，并且以 null 结尾。

```cpp

// Incorrect
void Func1(_Out_ PSTR pFileName, size_t n);

// Correct
void Func2(_Out_writes_(n) PSTR wszFileName, size_t n);
```

诸如 `_In_ PCSTR` 等批注很常见和有用。 它指向具有 NULL 终止的输入字符串，因为 `_In_` 的前置条件允许识别以 null 结尾的字符串。

## <a name="_in_-wchar-p"></a>\_In\_ WCHAR * p

`_In_ WCHAR* p` 声明具有指向一个字符的输入指针 `p`。 但是，在大多数情况下，这可能不是预期的规范。 预期的可能是以 null 结尾的数组的规范；为此，请使用 `_In_ PWSTR`。

```cpp

// Incorrect
void Func1(_In_ WCHAR* wszFileName);

// Correct
void Func2(_In_ PWSTR wszFileName);
```

缺少 NULL 终止的正确规范很常见。 如下面的示例所示，请使用相应的 `STR` 版本来替换类型。

```cpp

// Incorrect
BOOL StrEquals1(_In_ PCHAR p1, _In_ PCHAR p2)
{
    return strcmp(p1, p2) == 0;
}

// Correct
BOOL StrEquals2(_In_ PSTR p1, _In_ PSTR p2)
{
    return strcmp(p1, p2) == 0;
}
```

## <a name="_out_range_"></a>\_超出\_范围\_

如果参数是一个指针，并且想要表示指针指向的元素值的范围，请使用 `_Deref_out_range_` 而不是 `_Out_range_`。 在下面的示例中，表示的是 *pcbFilled 的范围，而不是 pcbFilled 的范围。

```cpp

// Incorrect
void Func1(
    _Out_writes_bytes_to_(cbSize, *pcbFilled) BYTE *pb,
    DWORD cbSize,
    _Out_range_(0, cbSize) DWORD *pcbFilled
);

// Correct
void Func2(
    _Out_writes_bytes_to_(cbSize, *pcbFilled) BYTE *pb,
    DWORD cbSize,
    _Deref_out_range_(0, cbSize) _Out_ DWORD *pcbFilled
);
```

一些工具并不是严格需要 `_Deref_out_range_(0, cbSize)`，因为它可从 `_Out_writes_to_(cbSize,*pcbFilled)` 推断，但为了完整性而将其显示在此处。

## <a name="wrong-context-in-_when_"></a>时出现错误\_的上下文\_

另一个常见错误是使用前置条件的状态后计算。 在下面的示例中，`_Requires_lock_held_` 是一个前置条件。

```cpp

// Incorrect
_When_(return == 0, _Requires_lock_held_(p->cs))
int Func1(_In_ MyData *p, int flag);

// Correct
_When_(flag == 0, _Requires_lock_held_(p->cs))
int Func2(_In_ MyData *p, int flag);
```

表达式 `result` 是指不适用于状态前的状态后值。

## <a name="true-in-_success_"></a>\_成功时为 TRUE\_

如果函数成功（范围值为非零），请使用 `return != 0` 作为成功条件，而不使用 `return == TRUE`。 非零不一定表示等于编译器为 `TRUE` 提供的实际值。 `_Success_` 的参数是一个表达式，并且以下表达式的计算结果相等：`return != 0`、`return != false`、`return != FALSE` 和 `return`（无参数或比较）。

```cpp

// Incorrect
_Success_(return == TRUE, _Acquires_lock_(*lpCriticalSection))
BOOL WINAPI TryEnterCriticalSection(
  _Inout_ LPCRITICAL_SECTION lpCriticalSection
);

// Correct
_Success_(return != 0, _Acquires_lock_(*lpCriticalSection))
BOOL WINAPI TryEnterCriticalSection(
  _Inout_ LPCRITICAL_SECTION lpCriticalSection
);
```

## <a name="reference-variable"></a>引用变量

对于引用变量，SAL 早期版本使用了隐式指针作为批注目标，并且需要向批注添加 `__deref` 以附加到引用变量。 此版本使用对象本身，不需要额外的 `_Deref_`。

```cpp

// Incorrect
void Func1(
    _Out_writes_bytes_all_(cbSize) BYTE *pb,
    _Deref_ _Out_range_(0, 2) _Out_ DWORD &cbSize
);

// Correct
void Func2(
    _Out_writes_bytes_all_(cbSize) BYTE *pb,
    _Out_range_(0, 2) _Out_ DWORD &cbSize
);
```

## <a name="annotations-on-return-values"></a>返回值的批注

下面的示例演示返回值批注中的一个常见问题。

```cpp

// Incorrect
_Out_opt_ void *MightReturnNullPtr1();

// Correct
_Ret_maybenull_ void *MightReturnNullPtr2();
```

在此示例中，`_Out_opt_` 声明作为前置条件的一部分，指针可以为 NULL。 但是，前置条件不能应用于返回值。 在这种情况下，正确的批注为 `_Ret_maybenull_`。

## <a name="see-also"></a>请参阅

[使用 SAL 批注以减少 C/C++ 代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)  
[了解 SAL](../code-quality/understanding-sal.md)  
[对函数参数和返回值进行批注](../code-quality/annotating-function-parameters-and-return-values.md)  
[对函数行为进行批注](../code-quality/annotating-function-behavior.md)  
[批注结构和类](../code-quality/annotating-structs-and-classes.md)  
[对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)  
[指定何时以及在何处应用批注](../code-quality/specifying-when-and-where-an-annotation-applies.md)  
[内部函数](../code-quality/intrinsic-functions.md)  
