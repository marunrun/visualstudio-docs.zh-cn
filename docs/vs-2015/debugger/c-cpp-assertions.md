---
title: C + + 断言 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
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
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9c26cc17d00881a72928806089a4c2880fdbce2f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702344"
---
# <a name="cc-assertions"></a>C/C++ 断言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

断言语句指定你预期程序中的某个点为 true 的条件。 如果该条件不为 true，则断言失败，程序执行中断并显示[“断言失败”对话框](../debugger/assertion-failed-dialog-box.md)。  

 Visual C++ 支持基于以下构造的断言语句：  

- MFC 程序的 MFC 断言。  

- 使用 ATL 的程序的 [ATLASSERT](https://msdn.microsoft.com/library/98e3e0fc-77e2-499b-a6f6-b17a21c6fbd3)。  

- 使用 C 运行时库的程序的 CRT 断言。  

- 其他 C/C++ 程序的 ANSI [assert 函数](https://msdn.microsoft.com/library/a9ca031a-648b-47a6-bdf1-65fc7399dd40)。  

  可以使用断言捕获逻辑错误、检查操作的结果以及测试应该已处理的错误条件。  

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> 在本主题中  
 [断言的工作方式](#BKMK_How_assertions_work)  

 [调试和发布生成中的断言](#BKMK_Assertions_in_Debug_and_Release_builds)  

 [使用断言的副作用](#BKMK_Side_effects_of_using_assertions)  

 [CRT 断言](#BKMK_CRT_assertions)  

 [MFC 断言](#BKMK_MFC_assertions)  

- [MFC ASSERT_VALID 和 CObject::AssertValid](#BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid)  

- [AssertValid 的限制](#BKMK_Limitations_of_AssertValid)  

  [使用断言](#BKMK_Using_assertions)  

- [捕获逻辑错误](#BKMK_Catching_logic_errors)  

- [检查结果](#BKMK_Checking_results_)  

- [查找未处理的错误](#BKMK_Testing_error_conditions_)  

## <a name="how-assertions-work"></a><a name="BKMK_How_assertions_work"></a> 断言的工作方式  
 当调试器由于 MFC 或 C 运行时库断言而暂停时，如果源可用，则它定位到源文件中的断言发生点。 断言消息显示在[输出窗口](../ide/reference/output-window.md)以及“断言失败”对话框中。 如果要保存断言消息以供将来参考，可以将断言消息从“输出”窗口复制到某个文本窗口。 输出窗口可能还包含其他错误信息。 请仔细检查这些消息，因为它们提供了断言失败原因的线索。  

 在开发过程中使用断言检测错误。 作为一种规则，对每个假设都使用一个断言。 例如，如果假设某个参数不为 NULL，则使用断言测试该假设。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="assertions-in-debug-and-release-builds"></a><a name="BKMK_Assertions_in_Debug_and_Release_builds"></a> 调试和发布生成中的断言  
 断言语句仅在定义了 `_DEBUG` 时才进行编译。 否则，编译器会将断言视为 null 语句。 因此，断言语句不会对最终发布程序施加开销或性能成本，使你可以避免使用 `#ifdef` 指令。  

## <a name="side-effects-of-using-assertions"></a><a name="BKMK_Side_effects_of_using_assertions"></a> 使用断言的副作用  
 将断言添加到代码时，确保断言没有副作用。 例如，考虑以下修改 `nM` 值的断言：  

```  
ASSERT(nM++ > 0); // Don't do this!  

```  

 由于不会在程序的发布版本中计算 `ASSERT` 表达式，因此 `nM` 在调试和发布版本中具有不同的值。 若要避免 MFC 中出现此问题，可以使用 [VERIFY](https://msdn.microsoft.com/library/3e1ab4ee-cbc7-4290-a777-c92f42ce7b96) 宏而不是 `ASSERT`。  `VERIFY` 会在所有版本中都计算表达式，但不检查发行版本中的结果。  

 请特别注意在断言语句中使用函数调用，因为计算函数可能会产生意外的副作用。  

```  
ASSERT ( myFnctn(0)==1 ) // unsafe if myFnctn has side effects  
VERIFY ( myFnctn(0)==1 ) // safe  
```  

 `VERIFY` 在调试版本和发布版本都会调用 `myFnctn`，以便它可以使用。 但是，使用 `VERIFY` 会在发布版本中施加不必要的函数调用开销。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="crt-assertions"></a><a name="BKMK_CRT_assertions"></a> CRT 断言  
 CRTDBG.H 头文件定义 [_ASSERT 和 _ASSERTE 宏](https://msdn.microsoft.com/library/e98fd2a6-7f5e-4aa8-8fe8-e93490deba36)用于断言检查。  

|   宏    |                                             结果                                              |
|------------|-------------------------------------------------------------------------------------------------|
| `_ASSERT`  | 如果指定表达式的计算结果为 FALSE，则为 `_ASSERT` 的文件名和行号。 |
| `_ASSERTE` |      与 `_ASSERT` 相同，再加上进行断言的表达式的字符串表示形式。       |

 `_ASSERTE` 功能更强大，因为它会报告结果为 FALSE 的断言表达式。 这可能足以确定问题，而无需参阅源代码。 但是，对于使用 `_ASSERTE` 进行断言的每个表达式，应用程序的调试版本都将包含一个字符串常数。 如果使用许多 `_ASSERTE` 宏，则这些字符串表达式会占用大量内存。 如果这证明有问题，请使用 `_ASSERT` 节省内存。  

 定义 `_DEBUG` 时，`_ASSERTE` 宏的定义如下：  

```  
#define _ASSERTE(expr) \  
   do { \  
      if (!(expr) && (1 == _CrtDbgReport( \  
         _CRT_ASSERT, __FILE__, __LINE__, #expr))) \  
         _CrtDbgBreak(); \  
   } while (0)  
```  

 如果断言表达式的计算结果为 FALSE，则会调用 [_CrtDbgReport](https://msdn.microsoft.com/library/6e581fb6-f7fb-4716-9432-f0145d639ecc) 以报告断言失败（默认情况下使用消息对话框）。 如果在消息对话框中选择“重试”，则 `_CrtDbgReport` 会返回 1，`_CrtDbgBreak` 会通过 `DebugBreak` 调用调试器。  

### <a name="checking-for-heap-corruption"></a>检查堆损坏  
 下面的示例使用 [_CrtCheckMemory](https://msdn.microsoft.com/library/457cc72e-60fd-4177-ab5c-6ae26a420765) 检查堆是否损坏：  

```  
_ASSERTE(_CrtCheckMemory());  
```  

### <a name="checking-pointer-validity"></a>检查指针有效性  
 下面的示例使用 [_CrtIsValidPointer](https://msdn.microsoft.com/library/91c35590-ea5e-450f-a15d-ad8d62ade1fa) 验证给定内存范围对于读取或写入是否有效。  

```  
_ASSERTE(_CrtIsValidPointer( address, size, TRUE );  
```  

 下面的示例使用 [_CrtIsValidHeapPointer](https://msdn.microsoft.com/library/caf597ce-1b05-4764-9f37-0197a982bec5) 验证指针是否指向本地堆中的内存（由 C 运行时库的此实例创建和管理的堆 — DLL 可以拥有自己的库实例，因此在应用程序堆之外拥有自己的堆）。 此断言不仅捕获 null 或超出界限地址，还捕获指向静态变量、堆栈变量和任何其他非本地内存的指针。  

```  
_ASSERTE(_CrtIsValidPointer( myData );  
```  

### <a name="checking-a-memory-block"></a>检查内存块  
 下面的示例使用 [_CrtIsMemoryBlock](https://msdn.microsoft.com/library/f7cbbc60-3690-4da0-a07b-68fd7f250273) 验证内存块是否处于本地堆中并且具有有效的块类型。  

```  
_ASSERTE(_CrtIsMemoryBlock (myData, size, &requestNumber, &filename, &linenumber));  
```  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="mfc-assertions"></a><a name="BKMK_MFC_assertions"></a> MFC 断言  
 MFC 定义 [ASSERT](https://msdn.microsoft.com/library/1e70902d-d58c-4e7b-9f69-2aeb6cbe476c) 宏以用于断言检查。 它还定义 `MFC ASSERT_VALID` 和 `CObject::AssertValid` 方法以用于检查 `CObject` 派生对象的内部状态。  

 如果 MFC `ASSERT` 宏的参数的计算结果为零或 false，则该宏会停止程序执行并向用户发出警报；否则，执行会继续。  

 当断言失败时，一个消息对话框会显示源文件的名称和断言的行号。 如果在该对话框中选择“重试”，则调用 [AfxDebugBreak](https://msdn.microsoft.com/library/c4cd79b9-9327-4db5-a9d6-c4004a92aa30) 会导致执行中断到调试器。 此时，可以检查调用堆栈，并使用其他调试器工具来确定断言失败的原因。 如果启用了[实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)并且调试器尚未运行，则该对话框可以启动调试器。  

 下面的示例演示如何使用 `ASSERT` 检查函数的返回值：  

```  
int x = SomeFunc(y);  
ASSERT(x >= 0);   //  Assertion fails if x is negative  
```  

 可以将 ASSERT 与 [IsKindOf](https://msdn.microsoft.com/library/7c87c748-b7e0-4c6d-9694-6035e62fdfd6) 函数一起使用，以提供函数参数的类型检查：  

```  
ASSERT( pObject1->IsKindOf( RUNTIME_CLASS( CPerson ) ) );  
```  

 在发布版本中，`ASSERT` 宏不生成任何代码。 如果需要在发布版本中计算表达式，请使用 [VERIFY](https://msdn.microsoft.com/library/3e1ab4ee-cbc7-4290-a777-c92f42ce7b96) 宏而不是 ASSERT。  

### <a name="mfc-assert_valid-and-cobjectassertvalid"></a><a name="BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid"></a> MFC ASSERT_VALID 和 CObject::AssertValid  
 [CObject::AssertValid](https://msdn.microsoft.com/library/534a0744-4ab6-423d-b492-b4058b3d5157) 方法提供对象内部状态的运行时检查。 尽管从 `CObject` 派生类时不需要替代 `AssertValid`，不过可以通过执行此操作使类更可靠。 `AssertValid` 应对对象的所有成员变量执行断言，以验证它们是否包含有效值。 例如，它应检查指针成员变量是否不为 NULL。  

 下面的示例演示如何声明 `AssertValid` 函数：  

```  
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

 替代 `AssertValid` 时，请先调用 `AssertValid` 的基类版本，然后再执行自己的检查。 随后使用 ASSERT 宏检查对派生类唯一的成员，如下所示：  

```  
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

 如果有任何成员变量存储对象，则可以使用 `ASSERT_VALID` 宏测试其内部有效性（如果它们的类会替代 `AssertValid`）。  

 例如，考虑一个类 `CMyData`，它将 [CObList](https://msdn.microsoft.com/library/80699c93-33d8-4f8b-b8cf-7b58aeab64ca) 存储在它的一个成员变量中。 `CObList` 变量 `m_DataList` 会存储 `CPerson` 对象的集合。 `CMyData` 的缩写声明如下所示：  

```  
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

 `CMyData` 中的 `AssertValid` 替代如下所示：  

```  
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

 `CMyData` 使用 `AssertValid` 机制测试其数据成员中存储的对象的有效性。 `CMyData` 的替代 `AssertValid` 会为其自己的 m_pDataList 成员变量调用 `ASSERT_VALID`。  

 有效性测试不会在此级别上停止，因为类 `CObList` 也会替代 `AssertValid`。 此替代会对列表的内部状态执行附加有效性测试。 因此，`CMyData` 对象上的有效性测试会对已存储 `CObList` 列表对象的内部状态形成附加有效性测试。  

 通过更多工作，还可以为存储在列表中的 `CPerson` 对象添加有效性测试。 可以从 `CObList` 派生类 `CPersonList`，并替代 `AssertValid`。 在替代中，会调用 `CObject::AssertValid`，然后循环访问列表，对列表中存储的每个 `CPerson` 对象调用 `AssertValid`。 本主题开头部分演示的 `CPerson` 类已替代 `AssertValid`。  

 在为调试进行生成时，这是一种功能强大的机制。 随后为发布进行生成时，该机制会自动关闭。  

### <a name="limitations-of-assertvalid"></a><a name="BKMK_Limitations_of_AssertValid"></a> AssertValid 的限制  
 触发的断言指示对象肯定有错误，执行将停止。 但是，没有断言仅指示未发现问题，但不保证对象正确。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="using-assertions"></a><a name="BKMK_Using_assertions"></a> 使用断言  

### <a name="catching-logic-errors"></a><a name="BKMK_Catching_logic_errors"></a> 捕获逻辑错误  
 可以根据程序的逻辑对必须为 true 的条件设置断言。 除非发生逻辑错误，否则断言不起作用。  

 例如，假设要模拟容器中的气体分子，而变量 `numMols` 表示分子的总数。 此数字不能小于零，因此可以包含如下所示的 MFC 断言语句：  

```  
ASSERT(numMols >= 0);  

```  

 或者，可以包含如下所示的 CRT 断言：  

```  
_ASSERT(numMols >= 0);  
```  

 如果程序运行正常，则这些语句不会执行任何操作。 但是，如果逻辑错误导致 `numMols` 小于零，则断言会停止程序执行，并显示[断言失败对话框](../debugger/assertion-failed-dialog-box.md)。  

 [在本主题中](#BKMK_In_this_topic)  

### <a name="checking-results"></a><a name="BKMK_Checking_results_"></a> 检查结果  
 对于测试无法通过快速的目视检查获得明显结果的操作，断言非常有用。  

 例如，考虑以下代码，它基于 `mols` 所指向的链接列表的内容来更新变量 `iMols`：  

```  
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

 由 `iMols` 计数的分子数必须始终小于或等于分子总数 `numMols`。 循环的目视检查并未表明这一定如此，因此在循环后使用断言语句来测试该条件。  

 [在本主题中](#BKMK_In_this_topic)  

### <a name="finding-unhandled-errors"></a><a name="BKMK_Testing_error_conditions_"></a> 查找未处理的错误  
 可以使用断言在代码中应已处理了所有错误的位置处测试是否存在错误条件。 在下面的示例中，一个图形例程返回错误代码或零（对于成功）。  

```  
myErr = myGraphRoutine(a, b);  

/* Code to handle errors and  
   reset myErr if successful */  

ASSERT(!myErr); -- MFC version  
_ASSERT(!myErr); -- CRT version  
```  

 如果错误处理代码正常工作，则在到达断言之前，错误应进行了处理并且 `myErr` 重置为零。 如果 `myErr` 具有其他值，则断言失败，程序会停止，并且[断言失败对话框](../debugger/assertion-failed-dialog-box.md)会出现。  

 不过，断言语句并不旨在替代错误处理代码。 下面的示例演示一个断言语句，它可能会导致最终发布代码中出现问题：  

```  
myErr = myGraphRoutine(a, b);  

/* No Code to handle errors */  

ASSERT(!myErr); // Don't do this!  
_ASSERT(!myErr); // Don't do this, either!  
```  

 此代码依赖于断言语句来处理错误条件。 因此，`myGraphRoutine` 返回的任何错误代码在最终发布代码中都未经处理。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="see-also"></a>另请参阅  
 [调试器安全性](../debugger/debugger-security.md)   
 [调试本机代码](../debugger/debugging-native-code.md)   
 [托管代码中的断言](../debugger/assertions-in-managed-code.md)
