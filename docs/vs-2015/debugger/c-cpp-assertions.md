---
title: C-C++断言 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
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

  可以使用断言来捕捉逻辑错误、 检查操作的结果和测试应处理的错误条件。  

## <a name="BKMK_In_this_topic"></a> 在本主题中  
 [断言的工作原理](#BKMK_How_assertions_work)  

 [调试和发布版本中的断言](#BKMK_Assertions_in_Debug_and_Release_builds)  

 [使用断言的副作用](#BKMK_Side_effects_of_using_assertions)  

 [CRT 断言](#BKMK_CRT_assertions)  

 [MFC 断言](#BKMK_MFC_assertions)  

- [MFC ASSERT_VALID 和 CObject::AssertValid](#BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid)  

- [AssertValid 的限制](#BKMK_Limitations_of_AssertValid)  

  [使用断言](#BKMK_Using_assertions)  

- [捕捉逻辑错误](#BKMK_Catching_logic_errors)  

- [检查结果](#BKMK_Checking_results_)  

- [查找未处理的错误](#BKMK_Testing_error_conditions_)  

## <a name="BKMK_How_assertions_work"></a> 断言的工作原理  
 当调试器由于 MFC 或 C 运行时库断言而停止时，如果源文件可用，则调试器将导航至源文件中的断言发生点。 断言消息显示在[输出窗口](../ide/reference/output-window.md) 和 **断言失败** 对话框中。 如果要保存断言消息以供将来参考，可以将断言消息从**输出**窗口复制到某个文本窗口。 **输出** 窗口可能还包含其他错误信息。 请仔细检查这些消息，因为它们提供了断言失败原因的线索。  

 使用断言来在开发过程中检测错误。 通常，对于每个假设使用一个断言。 例如，如果假定参数不是 NULL，请使用断言测试这种假设。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="BKMK_Assertions_in_Debug_and_Release_builds"></a> 调试和发布版本中的断言  
 断言语句编译仅当`_DEBUG`定义。 否则，编译器将断言作为空语句。 因此，断言语句会施加任何开销或性能成本在最终版本程序中，并允许您避免使用`#ifdef`指令。  

## <a name="BKMK_Side_effects_of_using_assertions"></a> 使用断言的副作用  
 当将断言添加到你的代码时，请确保断言不产生负面影响。 例如，考虑下面修改的断言`nM`值：  

```  
ASSERT(nM++ > 0); // Don't do this!  

```  

 因为`ASSERT`应用程序的发行版本中不计算表达式`nM`调试和发布版本中将具有不同的值。 若要避免此问题在 MFC 中的，可以使用[验证](https://msdn.microsoft.com/library/3e1ab4ee-cbc7-4290-a777-c92f42ce7b96)而不是宏`ASSERT`。  `VERIFY` 在所有版本中的表达式的计算结果，但不会检查发行版本中的结果。  

 应特别小心断言语句中使用函数调用，因为计算函数可能会有意外的副作用。  

```  
ASSERT ( myFnctn(0)==1 ) // unsafe if myFnctn has side effects  
VERIFY ( myFnctn(0)==1 ) // safe  
```  

 `VERIFY` 调用`myFnctn`在调试和发布版本中，因此是可接受的使用。 但是，使用`VERIFY`施加的发行版中的不必要的函数调用的开销。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="BKMK_CRT_assertions"></a> CRT 断言  
 CRTDBG。H 标头文件定义[_ASSERT 和 _ASSERTE 宏](https://msdn.microsoft.com/library/e98fd2a6-7f5e-4aa8-8fe8-e93490deba36)断言检查。  

|   宏    |                                             结果                                              |
|------------|-------------------------------------------------------------------------------------------------|
| `_ASSERT`  | 如果指定的表达式的计算结果为 FALSE 时，文件名称和行号的`_ASSERT`。 |
| `_ASSERTE` |      与相同`_ASSERT`，以及添加表达式的字符串表示形式。       |

 `_ASSERTE` 因为它可以报告是 FALSE 断言的表达式是更强大。 这可能不足以确定此问题，而不引用的源代码。 但是，你的应用程序的调试版本将包含断言使用每个表达式的字符串常数`_ASSERTE`。 如果您使用许多`_ASSERTE`宏，这些字符串表达式将占用大量内存。 如果，但事实证明，是一个问题，使用`_ASSERT`为了节省内存。  

 当`_DEBUG`定义，则`_ASSERTE`宏的定义如下：  

```  
#define _ASSERTE(expr) \  
   do { \  
      if (!(expr) && (1 == _CrtDbgReport( \  
         _CRT_ASSERT, __FILE__, __LINE__, #expr))) \  
         _CrtDbgBreak(); \  
   } while (0)  
```  

 如果断言的表达式的计算结果为 FALSE 时， [_CrtDbgReport](https://msdn.microsoft.com/library/6e581fb6-f7fb-4716-9432-f0145d639ecc)调用以报告断言失败 （默认情况下使用消息对话框）。 如果愿意**重试**消息对话框中`_CrtDbgReport`返回 1 和`_CrtDbgBreak`调用通过调试器`DebugBreak`。  

### <a name="checking-for-heap-corruption"></a>检查堆损坏  
 下面的示例使用[_CrtCheckMemory](https://msdn.microsoft.com/library/457cc72e-60fd-4177-ab5c-6ae26a420765)若要查看的堆已损坏：  

```  
_ASSERTE(_CrtCheckMemory());  
```  

### <a name="checking-pointer-validity"></a>检查指针有效性  
 下面的示例使用[_CrtIsValidPointer](https://msdn.microsoft.com/library/91c35590-ea5e-450f-a15d-ad8d62ade1fa)验证给定的内存范围是否有效用于读取或写入。  

```  
_ASSERTE(_CrtIsValidPointer( address, size, TRUE );  
```  

 下面的示例使用[_CrtIsValidHeapPointer](https://msdn.microsoft.com/library/caf597ce-1b05-4764-9f37-0197a982bec5)要验证是否一个指针，指向位于本地堆的内存 (堆创建和管理 C 运行时库的此实例的 — DLL 可以有自己的库，实例和因此自己堆，外部应用程序堆）。 此断言不会捕获仅为 null 或超出边界的地址，但还指向静态变量、 堆栈变量和任何其他非本地内存的指针。  

```  
_ASSERTE(_CrtIsValidPointer( myData );  
```  

### <a name="checking-a-memory-block"></a>正在检查的内存块  
 下面的示例使用[_CrtIsMemoryBlock](https://msdn.microsoft.com/library/f7cbbc60-3690-4da0-a07b-68fd7f250273)若要验证的内存块是否位于本地堆，并且具有有效的块类型。  

```  
_ASSERTE(_CrtIsMemoryBlock (myData, size, &requestNumber, &filename, &linenumber));  
```  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="BKMK_MFC_assertions"></a> MFC 断言  
 定义 MFC [ASSERT](https://msdn.microsoft.com/library/1e70902d-d58c-4e7b-9f69-2aeb6cbe476c)宏用于断言检查。 它还定义了`MFC ASSERT_VALID`并`CObject::AssertValid`方法用于检查的内部状态`CObject`-派生的对象。  

 如果参数的 MFC`ASSERT`宏计算结果为零或为 false，宏将暂停程序执行并警告用户; 否则，继续执行。  

 当一个断言失败时，消息对话框显示的名称的源文件和断言的行号。 如果在对话框中选择重试框中，调用[AfxDebugBreak](https://msdn.microsoft.com/library/c4cd79b9-9327-4db5-a9d6-c4004a92aa30)会导致执行中断到调试器。 此时，你可以检查调用堆栈和其他调试器功能用于确定断言失败的原因。 如果已启用[中实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)，并且调试器已不在运行，该对话框可以启动调试器。  

 下面的示例演示如何使用`ASSERT`检查函数的返回值：  

```  
int x = SomeFunc(y);  
ASSERT(x >= 0);   //  Assertion fails if x is negative  
```  

 可以使用与断言[IsKindOf](https://msdn.microsoft.com/library/7c87c748-b7e0-4c6d-9694-6035e62fdfd6)函数以提供类型检查函数自变量：  

```  
ASSERT( pObject1->IsKindOf( RUNTIME_CLASS( CPerson ) ) );  
```  

 `ASSERT`宏生成发布版本中的任何代码。 如果你需要评估的发行版本中的表达式，使用[验证](https://msdn.microsoft.com/library/3e1ab4ee-cbc7-4290-a777-c92f42ce7b96)宏而不是断言。  

### <a name="BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid"></a> MFC ASSERT_VALID 和 CObject::AssertValid  
 [CObject::AssertValid](https://msdn.microsoft.com/library/534a0744-4ab6-423d-b492-b4058b3d5157)方法提供了运行时检查的对象的内部状态。 虽然不需要重写`AssertValid`从类派生时`CObject`，您可以使您的类更加可靠通过执行此操作。 `AssertValid` 应在所有对象的成员变量，以验证它们包含有效的值都执行断言。 例如，它应检查指针成员变量不为 NULL。  

 下面的示例演示如何声明`AssertValid`函数：  

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

 当您重写`AssertValid`，调用基类版本的`AssertValid`执行您自己的检查之前。 然后使用 ASSERT 宏检查对派生类中，唯一的成员，如下所示：  

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

 如果任何成员变量存储对象，则可以使用`ASSERT_VALID`宏来测试其内部的有效性 (如果它们的类重写`AssertValid`)。  

 例如，考虑一个类`CMyData`，哪些商店[CObList](https://msdn.microsoft.com/library/80699c93-33d8-4f8b-b8cf-7b58aeab64ca)一个其成员变量中。 `CObList`变量， `m_DataList`，将存储一系列`CPerson`对象。 简化的声明`CMyData`如下所示：  

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

 `AssertValid`重写中`CMyData`如下所示：  

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

 `CMyData` 使用`AssertValid`机制以测试其数据成员中存储的对象的有效性。 重写`AssertValid`的`CMyData`调用`ASSERT_VALID`自己 m_pDataList 成员变量的宏。  

 有效性测试不会停止在此级别因为该类`CObList`还将重写`AssertValid`。 此替代执行附加有效性测试列表的内部状态。 因此，有效性测试上`CMyData`对象会导致存储的内部状态的其他有效性测试`CObList`列表对象。  

 更多工作，还可以添加对的有效性测试`CPerson`也存储在列表中的对象。 无法派生一个类`CPersonList`从`CObList`并重写`AssertValid`。 在重写时，会调用`CObject::AssertValid`，然后循环访问列表中，调用`AssertValid`每个`CPerson`对象存储在列表中。 `CPerson`类开头所示的本主题已重写`AssertValid`。  

 生成用于调试时，这是功能强大的机制。 当随后生成发布版本时，该机制是自动关闭。  

### <a name="BKMK_Limitations_of_AssertValid"></a> AssertValid 的限制  
 触发的断言指示对象是一定有误，将停止执行。 但是，缺乏断言仅指示将未找到任何问题，但该对象不能保证无法正常工作。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="BKMK_Using_assertions"></a> 使用断言  

### <a name="BKMK_Catching_logic_errors"></a> 捕捉逻辑错误  
 必须根据您的程序的逻辑，则返回 true 的条件，可以设置断言。 除非出现逻辑错误，则断言无效。  

 例如，假设您正在模拟中一个容器，而变量天然气分子`numMols`表示分子的总数。 此数字不能小于零，因此，可能包括 MFC 断言语句如下：  

```  
ASSERT(numMols >= 0);  

```  

 或者，可能包括如下的 CRT 断言：  

```  
_ASSERT(numMols >= 0);  
```  

 如果您的程序正常运行这些语句不执行任何操作。 如果逻辑错误导致`numMols`小于零，但是，则断言会中止程序的执行并显示[断言失败对话框](../debugger/assertion-failed-dialog-box.md)。  

 [在本主题中](#BKMK_In_this_topic)  

### <a name="BKMK_Checking_results_"></a> 检查结果  
 声明是用于测试的操作的结果不是从快速可视化检查明显有价值。  

 例如，考虑下面的代码，这会更新该变量`iMols`基于内容的链接列表指向的`mols`:  

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

 分子数的差除以`iMols`必须始终为小于或等于分子，总数`numMols`。 循环的可视化检查不显示，这一定将这种情况，因此断言语句循环后使用测试该条件。  

 [在本主题中](#BKMK_In_this_topic)  

### <a name="BKMK_Testing_error_conditions_"></a> 查找未处理的错误  
 可以使用断言来测试点的错误条件在代码中的任何错误应已处理。 在以下示例中，图形例程将返回错误代码或零表示成功。  

```  
myErr = myGraphRoutine(a, b);  

/* Code to handle errors and  
   reset myErr if successful */  

ASSERT(!myErr); -- MFC version  
_ASSERT(!myErr); -- CRT version  
```  

 如果错误处理代码是否正常运行，应处理错误和`myErr`重置为零之前达到断言。 如果`myErr`具有另一个值，则断言失败，程序暂停，并[断言失败对话框](../debugger/assertion-failed-dialog-box.md)出现。  

 断言语句不能代替有关错误处理代码，但是。 下面的示例显示了可能会导致问题的最终版本代码中的断言语句：  

```  
myErr = myGraphRoutine(a, b);  

/* No Code to handle errors */  

ASSERT(!myErr); // Don't do this!  
_ASSERT(!myErr); // Don't do this, either!  
```  

 此代码依赖于断言语句来处理错误条件。 因此，任何错误代码返回`myGraphRoutine`将在最终发行代码中未经处理。  

 [在本主题中](#BKMK_In_this_topic)  

## <a name="see-also"></a>请参阅  
 [调试器安全](../debugger/debugger-security.md)   
 [调试本机代码](../debugger/debugging-native-code.md)   
 [托管代码中的断言](../debugger/assertions-in-managed-code.md)
