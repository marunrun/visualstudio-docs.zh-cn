---
title: C/C++ 断言 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [MFC], assertions
- results, checking
- result checking
- Call Stack window, assertion failures
- debugging [C++], assertions
- VERIFY macro
- assertions, side effects
- assertions
- ASSERT macro
- errors [C++], catching with assertions
- testing, error conditions with assertion statements
- _DEBUG macro
- Assertion Failed dialog box
- failures, finding locations
ms.assetid: 2d7b0121-71aa-414b-bbb6-ede1093d0bfc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 154abe3d73fa71ac897f0442697196cd859f32bd
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72435888"
---
# <a name="cc-assertions"></a>C/C++ 断言
断言语句指定你预期程序中的某个点为 true 的条件。 如果该条件不为 true，则断言失败，程序执行中断并显示[“断言失败”对话框](../debugger/assertion-failed-dialog-box.md)。

Visual Studio 支持C++基于以下构造的断言语句：

- MFC 程序的 MFC 断言。

- 使用 ATL 的程序的 [ATLASSERT](/cpp/atl/reference/debugging-and-error-reporting-macros#atlassert)。

- 使用 C 运行时库的程序的 CRT 断言。

- 其他 C/C++ 程序的 ANSI [assert 函数](/cpp/c-runtime-library/reference/assert-macro-assert-wassert)。

  您可以使用断言来捕获逻辑错误、检查操作的结果和测试应该已处理的错误条件。

## <a name="BKMK_In_this_topic"></a> 在本主题中
[断言的工作方式](#BKMK_How_assertions_work)

[调试和发布版本中的断言](#BKMK_Assertions_in_Debug_and_Release_builds)

[使用断言的副作用](#BKMK_Side_effects_of_using_assertions)

[CRT 断言](#BKMK_CRT_assertions)

[MFC 断言](#BKMK_MFC_assertions)

- [MFC ASSERT_VALID 和 CObject：： AssertValid](#BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid)

- [AssertValid 的限制](#BKMK_Limitations_of_AssertValid)

  [使用断言](#BKMK_Using_assertions)

- [捕获逻辑错误](#BKMK_Catching_logic_errors)

- [检查结果](#BKMK_Checking_results_)

- [查找未处理的错误](#BKMK_Testing_error_conditions_)

## <a name="BKMK_How_assertions_work"></a>断言的工作方式
当调试器由于 MFC 或 C 运行时库断言而暂停时，如果源可用，则它定位到源文件中的断言发生点。 断言消息显示在[输出窗口](../ide/reference/output-window.md)以及“断言失败”对话框中。 如果要保存断言消息以供将来参考，可以将断言消息从“输出”窗口复制到某个文本窗口。 输出窗口可能还包含其他错误信息。 请仔细检查这些消息，因为它们提供了断言失败原因的线索。

使用断言来检测开发过程中的错误。 作为一种规则，对每个假设使用一个断言。 例如，如果假设某个参数不为 NULL，则使用断言测试该假设。

[主题内容](#BKMK_In_this_topic)

## <a name="BKMK_Assertions_in_Debug_and_Release_builds"></a>调试和发布版本中的断言
断言语句仅在定义 `_DEBUG` 时才编译。 否则，编译器会将断言视为 null 语句。 因此，断言语句不会对最终发布程序施加开销或性能成本，并使您可以避免使用 `#ifdef` 指令。

## <a name="BKMK_Side_effects_of_using_assertions"></a>使用断言的副作用
将断言添加到代码中时，请确保断言没有副作用。 例如，请考虑以下用于修改 `nM` 值的断言：

```cpp
ASSERT(nM++ > 0); // Don't do this!
```

由于不会在程序的发行版中计算 `ASSERT` 表达式，因此 `nM` 在调试和发布版本中具有不同的值。 若要避免 MFC 中出现此问题，可以使用[VERIFY](/cpp/mfc/reference/diagnostic-services#verify)宏而不是 `ASSERT`。 `VERIFY` 在所有版本中计算表达式的值，但不会在发布版本中检查结果。

请特别注意在断言语句中使用函数调用，因为计算函数可能会产生意外的副作用。

```cpp
ASSERT ( myFnctn(0)==1 ) // unsafe if myFnctn has side effects
VERIFY ( myFnctn(0)==1 ) // safe
```

`VERIFY` 调用调试版本和发布版本中 `myFnctn`，因此可接受使用。 但是，使用 `VERIFY` 会在发布版本中施加不必要的函数调用的开销。

[主题内容](#BKMK_In_this_topic)

## <a name="BKMK_CRT_assertions"></a>CRT 断言
CRTDBG.H。H 头文件定义用于断言检查的[_ASSERT 和 _ASSERTE 宏](/cpp/c-runtime-library/reference/assert-asserte-assert-expr-macros)。

| 宏 | 结果 |
|------------| - |
| `_ASSERT` | 如果指定的表达式的计算结果为 FALSE，则为 `_ASSERT` 的文件名和行号。 |
| `_ASSERTE` | 与 `_ASSERT` 相同，再加上已断言的表达式的字符串表示形式。 |

`_ASSERTE` 更为强大，因为它会报告声明为 FALSE 的断言表达式。 这可能足以识别问题，而无需引用源代码。 但是，应用程序的调试版本将包含使用 `_ASSERTE` 断言的每个表达式的字符串常量。 如果使用多个 `_ASSERTE` 宏，则这些字符串表达式占用大量内存。 如果这证明有问题，请使用 `_ASSERT` 来节省内存。

定义 `_DEBUG` 时，`_ASSERTE` 宏的定义如下：

```cpp
#define _ASSERTE(expr) \
    do { \
        if (!(expr) && (1 == _CrtDbgReport( \
            _CRT_ASSERT, __FILE__, __LINE__, #expr))) \
            _CrtDbgBreak(); \
    } while (0)
```

如果断言的表达式的计算结果为 FALSE，则会调用[_CrtDbgReport](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw)来报告断言失败（默认情况下使用消息对话框）。 如果在 "消息" 对话框中选择 "**重试**"，`_CrtDbgReport` 将返回1，`_CrtDbgBreak` 通过 `DebugBreak` 调用调试器。

### <a name="checking-for-heap-corruption"></a>检查堆损坏
下面的示例使用[_CrtCheckMemory](/cpp/c-runtime-library/reference/crtcheckmemory)检查堆是否损坏：

```cpp
_ASSERTE(_CrtCheckMemory());
```

### <a name="checking-pointer-validity"></a>检查指针有效性
下面的示例使用[_CrtIsValidPointer](/cpp/c-runtime-library/reference/crtisvalidpointer)来验证给定的内存范围对于读取或写入是有效的。

```cpp
_ASSERTE(_CrtIsValidPointer( address, size, TRUE );
```

下面的示例使用[_CrtIsValidHeapPointer](/cpp/c-runtime-library/reference/crtisvalidheappointer)来验证指针是否指向本地堆中的内存（由 C 运行时库的此实例创建和管理的堆），DLL 可以具有其自己的库实例，也可以是其自己的堆，在应用程序堆之外）。 此断言不仅捕获空或超出界限地址，还捕获指向静态变量、堆栈变量和任何其他非本地内存的指针。

```cpp
_ASSERTE(_CrtIsValidPointer( myData );
```

### <a name="checking-a-memory-block"></a>检查内存块
下面的示例使用[_CrtIsMemoryBlock](/cpp/c-runtime-library/reference/crtismemoryblock)来验证内存块是否位于本地堆中并且具有有效的块类型。

```cpp
_ASSERTE(_CrtIsMemoryBlock (myData, size, &requestNumber, &filename, &linenumber));
```

[主题内容](#BKMK_In_this_topic)

## <a name="BKMK_MFC_assertions"></a>MFC 断言
MFC 定义断言[宏用于断言检查](https://msdn.microsoft.com/Library/1e70902d-d58c-4e7b-9f69-2aeb6cbe476c)。 它还定义了用于检查 `CObject` 派生对象的内部状态的 `MFC ASSERT_VALID` 和 `CObject::AssertValid` 方法。

如果 MFC `ASSERT` 宏的参数的计算结果为零或 false，宏将暂停程序执行并向用户发出警报。否则，继续执行。

当断言失败时，将显示一个消息对话框，其中显示了该断言的源文件名和行号。 如果在对话框中选择 "重试"，则调用[AfxDebugBreak](/cpp/mfc/reference/diagnostic-services#afxdebugbreak)会导致执行中断到调试器。 此时，可以检查调用堆栈，并使用其他调试器工具来确定断言失败的原因。 如果已启用[实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)，并且调试器尚未运行，则该对话框可以启动调试器。

下面的示例演示如何使用 `ASSERT` 来检查函数的返回值：

```cpp
int x = SomeFunc(y);
ASSERT(x >= 0);   //  Assertion fails if x is negative
```

可以通过[IsKindOf](https://docs.microsoft.com/cpp/mfc/reference/cobject-class#iskindof)函数使用 ASSERT 来提供函数参数的类型检查：

```cpp
ASSERT( pObject1->IsKindOf( RUNTIME_CLASS( CPerson ) ) );
```

在发布版本中，`ASSERT` 宏不生成任何代码。 如果需要在发布版本中计算表达式，请使用[VERIFY](https://msdn.microsoft.com/library/s8c29sw2.aspx#verify)宏而不是 ASSERT。

### <a name="BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid"></a>MFC ASSERT_VALID 和 CObject：： AssertValid
[CObject：： AssertValid](https://docs.microsoft.com/cpp/mfc/reference/cobject-class#assertvalid)方法提供对对象的内部状态的运行时检查。 尽管从 `CObject` 派生类时不需要重写 `AssertValid`，但你可以通过执行此操作使类更可靠。 `AssertValid` 应对对象的所有成员变量执行断言，以验证它们是否包含有效的值。 例如，它应检查指针成员变量是否不为 NULL。

下面的示例演示如何声明一个 `AssertValid` 函数：

```cpp
class CPerson : public CObject
{
protected:
    CString m_strName;
    float   m_salary;
public:
#ifdef _DEBUG
    // Override
    virtual void AssertValid() const;
#endif
    // ...
};
```

重写 `AssertValid` 时，请先调用 `AssertValid` 的基类版本，然后再执行自己的检查。 然后，使用 ASSERT 宏来检查派生类的唯一成员，如下所示：

```cpp
#ifdef _DEBUG
void CPerson::AssertValid() const
{
    // Call inherited AssertValid first.
    CObject::AssertValid();

    // Check CPerson members...
    // Must have a name.
    ASSERT( !m_strName.IsEmpty());
    // Must have an income.
    ASSERT( m_salary > 0 );
}
#endif
```

如果任何成员变量存储对象，则可以使用 `ASSERT_VALID` 宏来测试其内部有效性（如果它们的类重写 `AssertValid`）。

例如，假设某个类 `CMyData`，它将[CObList](/cpp/mfc/reference/coblist-class)存储在它的一个成员变量中。 @No__t_0 变量 `m_DataList` 存储 `CPerson` 对象的集合。 @No__t_0 的缩写声明如下所示：

```cpp
class CMyData : public CObject
{
    // Constructor and other members ...
    protected:
        CObList* m_pDataList;
    // Other declarations ...
    public:
#ifdef _DEBUG
        // Override:
        virtual void AssertValid( ) const;
#endif
    // And so on ...
};
```

@No__t_1 中的 `AssertValid` 重写如下所示：

```cpp
#ifdef _DEBUG
void CMyData::AssertValid( ) const
{
    // Call inherited AssertValid.
    CObject::AssertValid( );
    // Check validity of CMyData members.
    ASSERT_VALID( m_pDataList );
    // ...
}
#endif
```

`CMyData` 使用 `AssertValid` 机制来测试其数据成员中存储的对象的有效性。 重写 `AssertValid` `CMyData` 将 `ASSERT_VALID` 宏用于其自己的 m_pDataList 成员变量。

不会在此级别停止有效性测试，因为类 `CObList` 还会覆盖 `AssertValid`。 此重写对列表的内部状态执行额外的有效性测试。 因此，`CMyData` 对象上的有效性测试将导致存储 `CObList` 列表对象的内部状态的其他有效性测试。

如果有更多工作，还可以为存储在列表中的 `CPerson` 对象添加有效性测试。 可以从 `CObList` 派生类，并替代 `AssertValid` `CPersonList`。 在替代中，你将调用 `CObject::AssertValid`，然后循环访问列表，并对列表中存储的每个 `CPerson` 对象调用 `AssertValid`。 本主题开头部分显示的 `CPerson` 类已经覆盖 `AssertValid`。

这是生成以进行调试时的一种强大机制。 当你随后生成以进行发布时，该机制会自动关闭。

### <a name="BKMK_Limitations_of_AssertValid"></a>AssertValid 的限制
触发的断言指示对象确实是错误的，执行将停止。 但是，如果缺少断言，则表明仅找不到任何问题，但不保证对象良好。

[主题内容](#BKMK_In_this_topic)

## <a name="BKMK_Using_assertions"></a>使用断言

### <a name="BKMK_Catching_logic_errors"></a>捕获逻辑错误
您可以根据程序的逻辑对必须为 true 的条件设置断言。 除非发生逻辑错误，否则断言不起作用。

例如，假设要模拟容器中的油门分子，而变量 `numMols` 表示分子的总数。 此数字不能小于零，因此你可能会包含如下所示的 MFC 断言语句：

```cpp
ASSERT(numMols >= 0);
```

或者，你可以包含如下 CRT 断言：

```cpp
_ASSERT(numMols >= 0);
```

如果程序运行正常，则这些语句不会执行任何操作。 但是，如果逻辑错误导致 `numMols` 小于零，则断言将暂停执行程序并显示 "[断言失败" 对话框](../debugger/assertion-failed-dialog-box.md)。

[主题内容](#BKMK_In_this_topic)

### <a name="BKMK_Checking_results_"></a>检查结果
断言对于测试其结果并不明显来自快速可视检查的操作非常有用。

例如，请考虑以下代码，该代码根据 `mols` 指向的链接列表的内容来更新变量 `iMols`。

```cpp
/* This code assumes that type has overloaded the != operator
 with const char *
It also assumes that H2O is somewhere in that linked list.
Otherwise we'll get an access violation... */
while (mols->type != "H2O")
{
    iMols += mols->num;
    mols = mols->next;
}
ASSERT(iMols<=numMols); // MFC version
_ASSERT(iMols<=numMols); // CRT version
```

@No__t_0 计数的分子数目必须始终小于或等于分子的总数 `numMols`。 循环的可视化检查并不表明这将是这样的，因此在循环后使用断言语句来测试该条件。

[主题内容](#BKMK_In_this_topic)

### <a name="BKMK_Testing_error_conditions_"></a>查找未处理的错误
您可以使用断言在代码中的某个时间点测试错误条件，这些错误条件应已处理。 在下面的示例中，图形例程返回错误代码，否则返回零。

```cpp
myErr = myGraphRoutine(a, b);

/* Code to handle errors and
   reset myErr if successful */

ASSERT(!myErr); -- MFC version
_ASSERT(!myErr); -- CRT version
```

如果错误处理代码正常工作，则应处理错误，并在达到断言之前 `myErr` 重置为零。 如果 `myErr` 有另一个值，则断言失败，程序将暂停，并显示 "[断言失败" 对话框](../debugger/assertion-failed-dialog-box.md)。

不过，断言语句并不替代错误处理代码。 下面的示例演示了一个断言语句，该语句可能导致最终发布代码中出现问题：

```cpp
myErr = myGraphRoutine(a, b);

/* No Code to handle errors */

ASSERT(!myErr); // Don't do this!
_ASSERT(!myErr); // Don't do this, either!
```

此代码依赖于断言语句来处理错误条件。 因此，`myGraphRoutine` 返回的任何错误代码将在最终发布代码中未经处理。

[主题内容](#BKMK_In_this_topic)

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [调试本机代码](../debugger/debugging-native-code.md)
- [托管代码中的断言](../debugger/assertions-in-managed-code.md)