---
title: 批注结构和类
ms.date: 06/28/2019
ms.topic: conceptual
f1_keywords:
- _Field_size_bytes_part_
- _Field_size_bytes_full_opt_
- _Field_size_bytes_
- _Field_size_opt_
- _Field_size_part_
- _Field_size_bytes_part_opt_
- _Field_range_
- _Field_size_part_opt_
- _Field_size_
- _Field_size_bytes_opt_
- _Struct_size_bytes_
- _Field_size_bytes_full_
- _Field_size_full_
- _Field_size_full_opt_
- _Field_z_
ms.assetid: b8278a4a-c86e-4845-aa2a-70da21a1dd52
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 35be465064c9524eb0e1339794b6a19b7a595da1
ms.sourcegitcommit: d2b234e0a4a875c3cba09321cdf246842670d872
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67493632"
---
# <a name="annotating-structs-and-classes"></a>批注结构和类

你可以通过使用类似于固定条件注释批注结构和类成员，它们都假定为满足的任何函数调用或进入/退出函数涉及封闭结构作为参数或结果值。

## <a name="struct-and-class-annotations"></a>结构和类批注

- `_Field_range_(low, high)`

     该字段是从 （含） 范围内`low`到`high`。  等效于`_Satisfies_(_Curr_ >= low && _Curr_ <= high)`通过使用适当的前置或后置条件应用于带批注的对象。

- `_Field_size_(size)`, `_Field_size_opt_(size)`, `_Field_size_bytes_(size)`, `_Field_size_bytes_opt_(size)`

     具有可写大小以元素 （或字节数） 为指定的字段`size`。

- `_Field_size_part_(size, count)`, `_Field_size_part_opt_(size, count)`,         `_Field_size_bytes_part_(size, count)`, `_Field_size_bytes_part_opt_(size, count)`

     具有可写大小以元素 （或字节数） 为指定的字段`size`，和`count`这些元素 （字节） 的可读。

- `_Field_size_full_(size)`, `_Field_size_full_opt_(size)`, `_Field_size_bytes_full_(size)`, `_Field_size_bytes_full_opt_(size)`

     具有可读和可写大小元素 （或字节数） 为指定的字段`size`。

- `_Field_z_`

     一个字段，具有一个以 null 结尾的字符串。

- `_Struct_size_bytes_(size)`

     适用于结构或类声明。  指示该类型的有效对象，可能与指定的字节数会大于声明的类型， `size`。  例如：

    ```cpp

    typedef _Struct_size_bytes_(nSize)
    struct MyStruct {
        size_t nSize;
        ...
    };

    ```

     以字节为单位的参数的缓冲区大小`pM`类型的`MyStruct *`然后将其视为：

    ```cpp
    min(pM->nSize, sizeof(MyStruct))
    ```

## <a name="example"></a>示例

```cpp
#include <sal.h>
// For FIELD_OFFSET macro
#include <windows.h>

// This _Struct_size_bytes_ is equivalent to what below _Field_size_ means.
_Struct_size_bytes_(FIELD_OFFSET(MyBuffer, buffer) + bufferSize * sizeof(int))
struct MyBuffer
{
    static int MaxBufferSize;
    
    _Field_z_
    const char* name;
    
    int firstField;

    // ... other fields

    _Field_range_(1, MaxBufferSize)
    int bufferSize;
    _Field_size_(bufferSize)        // Prefered way - easier to read and maintain.
    int buffer[0];
};
```

此示例中的说明：

- `_Field_z_` 与 `_Null_terminated_` 相等。  `_Field_z_` 名称字段指定名称字段，是一个以 null 结尾的字符串。
- `_Field_range_` 有关`bufferSize`指定的值`bufferSize`应在 1 和`MaxBufferSize`（均含）。
- 最终结果`_Struct_size_bytes_`和`_Field_size_`是等效的批注。 结构或类具有相似的布局`_Field_size_`更容易阅读和维护，因为它具有较少的引用和比等效的计算`_Struct_size_bytes_`批注。 `_Field_size_` 不需要转换为字节大小。 如果字节大小是唯一的选项，例如，对于 void 指针字段，`_Field_size_bytes_`可用。 如果这两个`_Struct_size_bytes_`和`_Field_size_`存在，同时将可供工具。 负责该工具要执行的操作如果不同意这两个批注。

## <a name="see-also"></a>请参阅

- [使用 SAL 批注以减少 C/C++ 代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [了解 SAL](../code-quality/understanding-sal.md)
- [对函数参数和返回值进行批注](../code-quality/annotating-function-parameters-and-return-values.md)
- [对函数行为进行批注](../code-quality/annotating-function-behavior.md)
- [对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)
- [指定何时以及在何处应用批注](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [内部函数](../code-quality/intrinsic-functions.md)
- [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)