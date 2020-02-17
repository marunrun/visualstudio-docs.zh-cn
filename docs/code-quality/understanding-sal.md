---
title: 了解 SAL
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: a94d6907-55f2-4874-9571-51d52d6edcfd
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: e2cb2cb263344e45d83a2b143f6c56f138f77bf5
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271823"
---
# <a name="understanding-sal"></a>了解 SAL

Microsoft 源代码注释语言（SAL）提供了一组可用于描述函数如何使用其参数的注释、对它们做出的假设，以及在完成时的保证。 批注是在标头文件 `<sal.h>`中定义的。 适用于的C++ Visual Studio 代码分析使用 SAL 批注来修改其函数分析。 有关适用于 Windows 驱动程序开发的 SAL 2.0 的详细信息，请参阅[Windows 驱动程序的 sal 2.0 注释](/windows-hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)。

对于开发人员而言C++ ，在本机和 C 中仅提供有限的方式，以一致的方式来表达意图和不变性。 通过使用 SAL 批注，可以更详细地描述函数，以便使用它们的开发人员可以更好地了解如何使用它们。

## <a name="what-is-sal-and-why-should-you-use-it"></a>什么是 SAL 以及您为何使用它?

简单地说，SAL 是一种成本较低的方法，使编译器能够为你检查代码。

### <a name="sal-makes-code-more-valuable"></a>SAL 使代码更重要

SAL 有助于使代码设计更易于理解，同时适用于用户和代码分析工具。 请考虑以下示例，其中显示了 C 运行时函数 `memcpy`：

```cpp

void * memcpy(
   void *dest,
   const void *src,
   size_t count
);
```

您能否知道此函数的作用？ 当实现或调用函数时，必须保持某些属性以确保程序的正确性。 只需查看示例中的声明，就不知道这些内容。 如果没有 SAL 批注，则必须依赖文档或代码注释。 下面是有关 `memcpy` 的 MSDN 文档的内容：

> "将计数字节的源复制到目标。 如果源和目标重叠，则 memcpy 的行为是不确定的。 使用 memmove 处理重叠区域。
> **安全说明：** 请确保目标缓冲区的大小等于或大于源缓冲区的大小。 有关详细信息，请参阅避免缓冲区溢出。

文档包含一些信息，这些信息表明你的代码必须维护某些属性以确保程序的正确性：

- `memcpy` 将字节的 `count` 从源缓冲区复制到目标缓冲区。

- 目标缓冲区的大小必须至少与源缓冲区的大小相同。

但编译器无法读取文档或非正式注释。 这并不知道两个缓冲区与 `count`之间存在关系，也不能有效地推测关系。 SAL 可以更清楚地了解函数的属性和实现，如下所示：

```cpp

void * memcpy(
   _Out_writes_bytes_all_(count) void *dest,
   _In_reads_bytes_(count) const void *src,
   size_t count
);
```

请注意，这些批注与 MSDN 文档中的信息类似，但它们更简洁，它们遵循语义模式。 阅读此代码后，你可以快速了解此函数的属性，以及如何避免缓冲区溢出的安全问题。 更好的是，SAL 提供的语义模式可以在潜在 bug 的早期发现中提高自动化代码分析工具的效率和有效性。 假设有人将此错误实现 `wmemcpy`：

```cpp

wchar_t * wmemcpy(
   _Out_writes_all_(count) wchar_t *dest,
   _In_reads_(count) const wchar_t *src,
   size_t count)
{
   size_t i;
   for (i = 0; i <= count; i++) { // BUG: off-by-one error
      dest[i] = src[i];
   }
   return dest;
}
```

此实现包含一个公共的、不是一个的错误。 幸运的是，代码作者包含 SAL 缓冲区大小注释，代码分析工具可通过单独分析此函数来捕获 bug。

### <a name="sal-basics"></a>SAL 基础
SAL 定义了四种基本类型的参数，这些参数按使用模式分类。

|类别|参数批注|说明|
|--------------|--------------------------|-----------------|
|**被调用函数的输入**|`_In_`|数据将传递给被调用的函数，并被视为只读。|
|**对被调用函数的输入和到调用方的输出**|`_Inout_`|可用数据将传递到函数中，并可能被修改。|
|**向调用方输出**|`_Out_`|调用方只为所调用的函数提供空间来写入。 被调用的函数将数据写入该空间。|
|**指向调用方的指针的输出**|`_Outptr_`|类似于**输出到调用方**。 被调用函数返回的值是一个指针。|

这四个基本批注可以通过多种方式进行更明确的了解。 默认情况下，使用批注指针参数是必需的，它们必须为非 NULL，函数才能成功。 基本批注最常使用的变体指示指针参数是可选的，如果该参数为 NULL，则该函数仍可成功执行其工作。

此表显示了如何区分必需参数和可选参数：

||参数是必需的|参数是可选的|
|-|-----------------------------|-----------------------------|
|**被调用函数的输入**|`_In_`|`_In_opt_`|
|**对被调用函数的输入和到调用方的输出**|`_Inout_`|`_Inout_opt_`|
|**向调用方输出**|`_Out_`|`_Out_opt_`|
|**指向调用方的指针的输出**|`_Outptr_`|`_Outptr_opt_`|

这些批注有助于识别可能未初始化的值，无效的空指针将以正式准确的方式使用。 将 NULL 传递给必需的参数可能会导致崩溃，否则可能会导致返回 "failed" 错误代码。 无论采用哪种方式，函数都不能成功执行其作业。

## <a name="sal-examples"></a>SAL 示例
此部分显示基本 SAL 批注的代码示例。

### <a name="using-the-visual-studio-code-analysis-tool-to-find-defects"></a>使用 Visual Studio 代码分析工具查找 Bug
在示例中，Visual Studio Code 分析工具与 SAL 注释一起用于查找代码缺陷。 下面介绍了如何执行此操作。

#### <a name="to-use-visual-studio-code-analysis-tools-and-sal"></a>使用 Visual Studio 代码分析工具和 SAL

1. 在 Visual Studio 中，打开C++包含 SAL 批注的项目。

2. 在菜单栏上，选择 "**生成**"、 **"对解决方案运行代码分析**"。

     请考虑本部分\_ 示例中的 \_。 如果对其运行代码分析，将显示以下警告：

    > **C6387 参数值无效**"指向" 可能是 "0"：这不符合函数 "InCallee" 的规范。

### <a name="example-the-_in_-annotation"></a>示例：\_ 批注中的 \_

`_In_` 批注指示：

- 参数必须有效且不会被修改。

- 函数将只从单元素缓冲区中读取。

- 调用方必须提供缓冲区并对其进行初始化。

- `_In_` 指定 "只读"。 常见的错误是将 `_In_` 应用于应改为 `_Inout_` 批注的参数。

- 在非指针标量上，分析器允许使用 `_In_` 但不允许使用。

```cpp
void InCallee(_In_ int *pInt)
{
   int i = *pInt;
}

void GoodInCaller()
{
   int *pInt = new int;
   *pInt = 5;

   InCallee(pInt);
   delete pInt;
}

void BadInCaller()
{
   int *pInt = NULL;
   InCallee(pInt); // pInt should not be NULL
}
```

如果在此示例中使用 Visual Studio Code 分析，它将验证调用方是否将非 Null 指针传递到 `pInt`的已初始化缓冲区。 在这种情况下，`pInt` 指针不能为 NULL。

### <a name="example-the-_in_opt_-annotation"></a>示例：\_opt\_ 批注中的 \_

`_In_opt_` 与 `_In_`相同，不同之处在于允许输入参数为 NULL，因此函数应检查此值。

```cpp

void GoodInOptCallee(_In_opt_ int *pInt)
{
   if(pInt != NULL) {
      int i = *pInt;
   }
}

void BadInOptCallee(_In_opt_ int *pInt)
{
   int i = *pInt; // Dereferencing NULL pointer 'pInt'
}

void InOptCaller()
{
   int *pInt = NULL;
   GoodInOptCallee(pInt);
   BadInOptCallee(pInt);
}
```

Visual Studio Code 分析验证函数在访问缓冲区之前是否检查是否为 NULL。

### <a name="example-the-_out_-annotation"></a>示例： \_Out\_ 批注

`_Out_` 支持一个常见情况，即在其中传递指向元素缓冲区的非 NULL 指针，并且该函数将初始化元素。 调用方无需在调用之前初始化缓冲区;被调用的函数承诺在返回之前对其进行初始化。

```cpp
void GoodOutCallee(_Out_ int *pInt)
{
   *pInt = 5;
}

void BadOutCallee(_Out_ int *pInt)
{
   // Did not initialize pInt buffer before returning!
}

void OutCaller()
{
   int *pInt = new int;
   GoodOutCallee(pInt);
   BadOutCallee(pInt);
   delete pInt;
}
```

Visual Studio Code 分析工具将验证调用方是否将非 NULL 指针传递到 `pInt` 的缓冲区，并验证该缓冲区是否在返回之前由函数进行了初始化。

### <a name="example-the-_out_opt_-annotation"></a>示例： \_Out\_opt\_ 批注

`_Out_opt_` 与 `_Out_`相同，不同之处在于允许参数为 NULL，因此该函数应检查此值。

```cpp
void GoodOutOptCallee(_Out_opt_ int *pInt)
{
   if (pInt != NULL) {
      *pInt = 5;
   }
}

void BadOutOptCallee(_Out_opt_ int *pInt)
{
   *pInt = 5; // Dereferencing NULL pointer 'pInt'
}

void OutOptCaller()
{
   int *pInt = NULL;
   GoodOutOptCallee(pInt);
   BadOutOptCallee(pInt);
}
```

Visual Studio Code 分析验证此函数在取消引用 `pInt` 之前是否检查 NULL，如果 `pInt` 不为 NULL，则该函数将在返回前通过函数初始化缓冲区。

### <a name="example-the-_inout_-annotation"></a>示例： \_Inout\_ 批注

`_Inout_` 用于批注可能由函数更改的指针参数。 指针必须指向有效的已初始化数据，然后才能调用，即使它发生更改，返回的值也必须有效。 批注指定函数可以从单元素缓冲区自由读取和写入。 调用方必须提供缓冲区并对其进行初始化。

> [!NOTE]
> 与 `_Out_`一样，`_Inout_` 必须应用于可修改的值。

```cpp
void InOutCallee(_Inout_ int *pInt)
{
   int i = *pInt;
   *pInt = 6;
}

void InOutCaller()
{
   int *pInt = new int;
   *pInt = 5;
   InOutCallee(pInt);
   delete pInt;
}

void BadInOutCaller()
{
   int *pInt = NULL;
   InOutCallee(pInt); // 'pInt' should not be NULL
}
```

Visual Studio Code 分析验证调用方将非 NULL 指针传递到 `pInt`的已初始化缓冲区，并且在返回之前，`pInt` 仍为非 NULL，并且已初始化缓冲区。

### <a name="example-the-_inout_opt_-annotation"></a>示例： \_Inout\_opt\_ 批注

`_Inout_opt_` 与 `_Inout_`相同，不同之处在于允许输入参数为 NULL，因此函数应检查此值。

```cpp
void GoodInOutOptCallee(_Inout_opt_ int *pInt)
{
   if(pInt != NULL) {
      int i = *pInt;
      *pInt = 6;
   }
}

void BadInOutOptCallee(_Inout_opt_ int *pInt)
{
   int i = *pInt; // Dereferencing NULL pointer 'pInt'
   *pInt = 6;
}

void InOutOptCaller()
{
   int *pInt = NULL;
   GoodInOutOptCallee(pInt);
   BadInOutOptCallee(pInt);
}
```

Visual Studio Code 分析验证此函数在访问缓冲区之前是否检查是否为 NULL，如果 `pInt` 不为 NULL，则该函数将在返回前通过函数初始化缓冲区。

### <a name="example-the-_outptr_-annotation"></a>示例： \_Outptr\_ 批注

`_Outptr_` 用于批注要返回指针的参数。  参数本身不应为 NULL，并且被调用的函数在其中返回非 NULL 指针，该指针指向已初始化的数据。

```cpp
void GoodOutPtrCallee(_Outptr_ int **pInt)
{
   int *pInt2 = new int;
   *pInt2 = 5;

   *pInt = pInt2;
}

void BadOutPtrCallee(_Outptr_ int **pInt)
{
   int *pInt2 = new int;
   // Did not initialize pInt buffer before returning!
   *pInt = pInt2;
}

void OutPtrCaller()
{
   int *pInt = NULL;
   GoodOutPtrCallee(&pInt);
   BadOutPtrCallee(&pInt);
}
```

Visual Studio Code 分析验证调用方传递 `*pInt`的非 NULL 指针，并验证该缓冲区是否在返回前由函数进行了初始化。

### <a name="example-the-_outptr_opt_-annotation"></a>示例： \_Outptr\_opt\_ 批注

`_Outptr_opt_` 与 `_Outptr_`相同，不同之处在于参数是可选的，调用方可以传入参数的 NULL 指针。

```cpp
void GoodOutPtrOptCallee(_Outptr_opt_ int **pInt)
{
   int *pInt2 = new int;
   *pInt2 = 6;

   if(pInt != NULL) {
      *pInt = pInt2;
   }
}

void BadOutPtrOptCallee(_Outptr_opt_ int **pInt)
{
   int *pInt2 = new int;
   *pInt2 = 6;
   *pInt = pInt2; // Dereferencing NULL pointer 'pInt'
}

void OutPtrOptCaller()
{
   int **ppInt = NULL;
   GoodOutPtrOptCallee(ppInt);
   BadOutPtrOptCallee(ppInt);
}
```

Visual Studio Code 分析验证此函数在取消引用 `*pInt` 之前是否检查 NULL，并验证该函数是否在返回之前由函数进行了初始化。

### <a name="example-the-_success_-annotation-in-combination-with-_out_"></a>示例： \_成功\_ 批注与 \_Out\_

批注可应用于大多数对象。  特别是，您可以批注整个函数。  函数最明显的特征之一是它可以成功或失败。 但就像缓冲区及其大小之间的关联，C/C++无法表示函数成功或失败。 通过使用 `_Success_` 注释，可以说出函数的成功情况。  `_Success_` 批注的参数只是一个表达式，表示函数已成功。 表达式可以是批注分析器可处理的任何内容。 当函数返回后，批注的效果仅适用于函数成功。 此示例演示 `_Success_` 如何与 `_Out_` 进行交互以执行正确的操作。 您可以使用关键字 `return` 来表示返回值。

```cpp
_Success_(return != false) // Can also be stated as _Success_(return)
bool GetValue(_Out_ int *pInt, bool flag)
{
   if(flag) {
      *pInt = 5;
      return true;
   } else {
      return false;
   }
}
```

`_Out_` 批注将导致 Visual Studio Code 分析验证调用方将非 NULL 指针传递到用于 `pInt`的缓冲区，并且该缓冲区在返回前由函数进行初始化。

## <a name="sal-best-practice"></a>SAL 最佳做法

### <a name="adding-annotations-to-existing-code"></a>向现有代码中添加批注

SAL 是一项功能强大的技术，可帮助您提高代码的安全性和可靠性。 了解 SAL 后，您可以将新技能应用于您的日常工作。 在新代码中，可以在整个设计中使用基于 SAL 的规范;在较旧的代码中，你可以递增地添加批注，因此，每次更新时都会增加权益。

Microsoft 公共标头已进行批注。 因此，我们建议在项目中首先批注叶节点函数和调用 Win32 Api 的函数以获得最大的好处。

### <a name="when-do-i-annotate"></a>何时批注?

下面是一些指导原则：

- 批注所有指针参数。

- 为值范围批注添加批注，以便代码分析可以确保缓冲区和指针安全性。

- 批注锁定规则和锁定副作用。 有关详细信息，请参阅对[锁定行为进行批注](../code-quality/annotating-locking-behavior.md)。

- 批注驱动程序属性和其他特定于域的属性。

或者，您可以为所有参数添加注释以使您的意图清晰明了，并使您能够轻松地检查批注是否已完成。

## <a name="related-resources"></a>相关资源

[代码分析团队博客](https://blogs.msdn.microsoft.com/codeanalysis/)

## <a name="see-also"></a>另请参阅

- [使用 SAL 批注以减少 C/C++ 代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [对函数参数和返回值进行批注](../code-quality/annotating-function-parameters-and-return-values.md)
- [对函数行为进行批注](../code-quality/annotating-function-behavior.md)
- [批注结构和类](../code-quality/annotating-structs-and-classes.md)
- [对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)
- [指定何时以及在何处应用批注](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)
