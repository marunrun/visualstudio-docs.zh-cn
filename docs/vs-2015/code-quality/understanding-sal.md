---
title: 了解 SAL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: a94d6907-55f2-4874-9571-51d52d6edcfd
caps.latest.revision: 20
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: 0a898096c282a22201d60995693144cc0e187812
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435400"
---
# <a name="understanding-sal"></a>了解 SAL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft 源代码注释语言 (SAL) 提供了一组可用于描述函数如何使用它的参数、 关于它们的假设和它对完成的保证的批注。 标头文件中定义批注`<sal.h>`。 Visual Studio 代码分析C++使用 SAL 注释来修改其分析函数。 Windows 驱动程序开发的 SAL 2.0 的详细信息，请参阅[SAL 2.0 注释为 Windows 驱动程序](http://go.microsoft.com/fwlink/?LinkId=250979)。  
  
 本机 C 和C++提供仅面向开发人员来一致地表达意图和不变性有限的方式。 通过使用 SAL 注释，可以描述中更详细地介绍函数，以便开发人员会使用这些资源可以更好地了解如何使用它们。  
  
## <a name="what-is-sal-and-why-should-you-use-it"></a>什么是 SAL 以及您为何使用它?  
 简单地说，SAL 是较低的方式让编译器为您检查您的代码。  
  
### <a name="sal-makes-code-more-valuable"></a>SAL 使代码更重要  
 SAL 可以帮助您使代码设计更易于理解，人类和代码分析工具。 请考虑此示例演示 C 运行时函数`memcpy`:  
  
```cpp  
  
void * memcpy(  
   void *dest,   
   const void *src,   
   size_t count  
);  
  
```  
  
 您是否能告诉该函数的？ 当一个函数是实现或调用时，必须维护的某些属性以确保程序的正确性。 只需通过查看声明如示例中，你不知道它们是什么。 如果没有 SAL 批注，您必须依赖于文档或代码注释。 下面是 MSDN 文档的`memcpy`说：  
  
> "副本计数字节到目标的 src。 如果源和目标重叠，memcpy 的行为未定义。 使用 memmove 处理重叠区域。   
> **安全说明：** 确保目标缓冲区等于或大于源缓冲区。 有关详细信息，请参阅避免缓冲区溢出。"  
  
 文档中包含几位的信息，建议你的代码具有要维护某些属性，以确保程序的正确性：  
  
- `memcpy` 副本`count`中的字节源缓冲区到目标缓冲区。  
  
- 目标缓冲区必须至少与源缓冲区一样大。  
  
  但是，编译器无法读取的文档或非正式注释。 它不知道两个缓冲区之间不存在关系和`count`，它也不能有效地猜猜有关关系。 SAL 可以提供更多更清晰的属性和函数的实现，如下所示：  
  
```cpp  
  
void * memcpy(  
   _Out_writes_bytes_all_(count) void *dest,   
   _In_reads_bytes_(count) const void *src,   
   size_t count  
);  
```  
  
 请注意，这些批注类似于 MSDN 文档中的信息，但更简洁，并且它们都遵循语义的模式。 阅读此代码，可以快速了解此函数的属性以及如何避免缓冲区溢出的安全问题。 更为可喜的是，SAL 提供的语义模式可以提高效率和效果在早期发现潜在的 bug 的自动的代码分析工具。 假设有人编写的这一错误实现`wmemcpy`:  
  
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
  
 此实现包含一种常见关闭--一个错误。 幸运的是，代码作者包含 SAL 缓冲区大小批注，代码分析工具无法通过分析此函数只捕获 bug。  
  
### <a name="sal-basics"></a>SAL 基础  
 SAL 定义四种基本类型的参数，按使用模式进行分类。  
  
|类别|参数批注|描述|  
|--------------|--------------------------|-----------------|  
|**对输入调用函数**|`_In_`|数据传递给被调用函数，并以只读方式处理。|  
|**对输入调用函数，并输出发送到调用方**|`_Inout_`|可以使用的数据传递到函数，并可能被修改。|  
|**输出到调用方**|`_Out_`|调用方仅提供要写入到的被调用函数的空间。 被调用的函数将数据写入到该空间。|  
|**指向调用方的输出**|`_Outptr_`|像**输出到调用方**。 被调用函数返回的值是一个指针。|  
  
 这些四个基本批注可以进行更显式以各种方式。 默认情况下，带批注的指针参数被假定为必需，它们必须为非 NULL 函数才会成功。 基本的批注的最常使用变体指示指针参数是可选的-如果，则为 NULL，该函数仍可以成功中执行其工作。  
  
 此表显示了如何区分必需和可选参数：  
  
||参数是必需的|参数是可选的|  
|-|-----------------------------|-----------------------------|  
|**对输入调用函数**|`_In_`|`_In_opt_`|  
|**对输入调用函数，并输出发送到调用方**|`_Inout_`|`_Inout_opt_`|  
|**输出到调用方**|`_Out_`|`_Out_opt_`|  
|**指向调用方的输出**|`_Outptr_`|`_Outptr_opt_`|  
  
 这些批注帮助识别可能未初始化的值，并正式且准确的方式使用无效的 null 指针。 将 NULL 传递到所需的参数可能会导致崩溃的原因，或它可能会导致要返回的"失败"，错误代码。 无论哪种方式，该函数中执行其作业不成功。  
  
## <a name="sal-examples"></a>SAL 示例  
 本部分展示了基本的 SAL 注释的代码示例。  
  
### <a name="using-the-visual-studio-code-analysis-tool-to-find-defects"></a>使用 Visual Studio 代码分析工具查找 Bug  
 在示例中，Visual Studio 代码分析工具是与一起使用 SAL 批注以查找代码缺陷。 下面介绍了如何执行此操作。  
  
##### <a name="to-use-visual-studio-code-analysis-tools-and-sal"></a>使用 Visual Studio 代码分析工具和 SAL  
  
1. 在 Visual Studio 中打开C++项目，其中包含 SAL 注释。  
  
2. 在菜单栏上依次选择**构建**，**对解决方案运行代码分析**。  
  
    请考虑\_在\_在本部分中的示例。 如果对其运行代码分析，则显示此警告：  
  
   > **C6387 无效的参数值**   
   > pInt 可能是"0": 这不符合函数 InCallee 的规范。  
  
### <a name="example-the-in-annotation"></a>示例:\_在\_批注  
 `_In_`批注指示：  
  
- 该参数必须是有效，并且不会被修改。  
  
- 该函数将只读取单个元素缓冲区中。  
  
- 调用方必须提供缓冲区，并对其进行初始化。  
  
- `_In_` 指定"只读"。 一个常见错误是应用`_In_`参数应具有`_Inout_`批注相反。  
  
- `_In_` 允许在非指针标量分析器但被忽略。  
  
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
  
 如果在此示例中使用 Visual Studio 代码分析，它会验证调用方将非 Null 指针传递给初始化缓冲区`pInt`。 在这种情况下，`pInt`指针不能为 NULL。  
  
### <a name="example-the-inopt-annotation"></a>示例:\_In_opt\_批注  
 `_In_opt_` 等同于`_In_`，只不过允许的输入的参数为 NULL，并且因此，该函数应检查这一点。  
  
```cpp  
  
void GoodInOptCallee(_In_opt_ int *pInt)  
{  
   if(pInt != NULL) {  
      int i = *pInt;  
   }  
}  
  
void BadInOptCallee(_In_opt_ int *pInt)  
{  
   int i = *pInt; // Dereferencing NULL pointer ‘pInt’  
}  
  
void InOptCaller()  
{  
   int *pInt = NULL;  
   GoodInOptCallee(pInt);  
   BadInOptCallee(pInt);  
}  
  
```  
  
 Visual Studio 代码分析会验证该函数检查为空，然后才能访问缓冲区。  
  
### <a name="example-the-out-annotation"></a>示例:\_出\_批注  
 `_Out_` 支持一种常见的方案，在其中传入指向的元素的缓冲区的非 NULL 指针和函数来初始化元素。 调用方没有调用; 之前将缓冲区初始化被调用的函数有望在返回之前对其进行初始化。  
  
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
  
 Visual Studio 代码分析工具验证调用方将非 NULL 指针传递到的缓冲区`pInt`并在返回之前，将缓冲区初始化函数。  
  
### <a name="example-the-outopt-annotation"></a>示例:\_Out_opt\_批注  
 `_Out_opt_` 等同于`_Out_`，只不过该参数是否可为 NULL，并且因此，该函数应检查这一点。  
  
```cpp  
  
void GoodOutOptCallee(_Out_opt_ int *pInt)  
{  
   if (pInt != NULL) {  
      *pInt = 5;  
   }  
}  
  
void BadOutOptCallee(_Out_opt_ int *pInt)  
{  
   *pInt = 5; // Dereferencing NULL pointer ‘pInt’  
}  
  
void OutOptCaller()  
{  
   int *pInt = NULL;  
   GoodOutOptCallee(pInt);  
   BadOutOptCallee(pInt);  
}  
  
```  
  
 Visual Studio 代码分析验证，此函数会检查是否在之前为空`pInt`被取消引用，并且如果`pInt`不为 NULL，在返回之前，该函数初始化缓冲区。  
  
### <a name="example-the-inout-annotation"></a>示例:\_Inout\_批注  
 `_Inout_` 用于进行批注可能会更改函数的指针参数。 指针必须指向有效的调用之前已初始化的数据，并且即使更改，仍必须有效的值返回。 批注指定函数可能会随意从读取和写入一个元素缓冲区。 调用方必须提供缓冲区，并对其进行初始化。  
  
> [!NOTE]
> 像`_Out_`，`_Inout_`必须将应用于可修改的值。  
  
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
   InOutCallee(pInt); // ‘pInt’ should not be NULL  
}  
  
```  
  
 Visual Studio 代码分析验证调用方将非 NULL 指针传递给初始化缓冲区`pInt`，并且，在返回时之前,`pInt`仍非 null 和缓冲区初始化。  
  
### <a name="example-the-inoutopt-annotation"></a>示例:\_Inout_opt\_批注  
 `_Inout_opt_` 等同于`_Inout_`，只不过允许的输入的参数为 NULL，并且因此，该函数应检查这一点。  
  
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
   int i = *pInt; // Dereferencing NULL pointer ‘pInt’  
   *pInt = 6;  
}  
  
void InOutOptCaller()  
{  
   int *pInt = NULL;  
   GoodInOutOptCallee(pInt);  
   BadInOutOptCallee(pInt);  
}  
  
```  
  
 Visual Studio 代码分析验证，此函数进行 NULL 检查，它将访问缓冲区之前，并且如果`pInt`不为 NULL，在返回之前，该函数初始化缓冲区。  
  
### <a name="example-the-outptr-annotation"></a>示例:\_Outptr\_批注  
 `_Outptr_` 用于批注的目的是要返回的指针参数。  参数本身不应为 NULL，和调用的函数中返回非 NULL 指针，该指针指向已初始化的数据。  
  
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
  
 Visual Studio 代码分析验证调用方传递非空指针`*pInt`，并在返回之前，将缓冲区初始化函数。  
  
### <a name="example-the-outptropt-annotation"></a>示例:\_Outptr_opt\_批注  
 `_Outptr_opt_` 等同于`_Outptr_`，只不过参数是可选的调用方可以传递给 NULL 指针的参数。  
  
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
   *pInt = pInt2; // Dereferencing NULL pointer ‘pInt’  
}  
  
void OutPtrOptCaller()  
{  
   int **ppInt = NULL;  
   GoodOutPtrOptCallee(ppInt);  
   BadOutPtrOptCallee(ppInt);  
}  
  
```  
  
 Visual Studio 代码分析验证此函数检查 null 之前`*pInt`被取消引用，并在返回之前，将缓冲区初始化函数。  
  
### <a name="example-the-success-annotation-in-combination-with-out"></a>示例:\_成功\_批注结合\_出\_  
 批注可以应用于大多数对象。  具体而言，你可以批注整个函数。  一个函数的最明显特征之一是它可以成功或失败。 但如缓冲区和其大小，C 之间的关联 /C++不能表达函数成功还是失败。 通过使用`_Success_`批注，您可以说，函数成功指数。  为参数`_Success_`批注是只是一个表达式，为 true 表示该函数已成功。 表达式可以是任何批注分析器可以处理。 如果此函数成功后该函数将返回, 的批注的效果才适用。 此示例演示如何`_Success_`与交互`_Out_`以执行正确的操作。 可以使用关键字`return`来表示返回值。  
  
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
  
 `_Out_`批注将导致 Visual Studio 代码分析来验证调用方将非 NULL 指针传递到的缓冲区`pInt`，并在返回之前，将缓冲区初始化函数。  
  
## <a name="sal-best-practice"></a>SAL 最佳做法  
  
### <a name="adding-annotations-to-existing-code"></a>向现有代码中添加批注  
 SAL 是代码的一种功能强大的技术，可帮助您提高安全性和可靠性。 了解 SAL 后，可以将新的技能应用到您的日常工作。 在新代码中，你可以通过基于 SAL 的规范; 在整个设计在较旧代码中，可以以增量方式添加批注和每次更新，从而提高效益。  
  
 Microsoft 公共标头已进行批注。 因此，我们建议，在项目中首先批注叶节点函数和函数调用 Win32 Api 来获取最大效益。  
  
### <a name="when-do-i-annotate"></a>何时批注?  
 以下是一些准则：  
  
- 批注所有指针参数。  
  
- 批注值范围批注，以便代码分析可确保缓冲区和指针安全。  
  
- 锁定规则和锁定的副作用批注。 有关详细信息，请参阅[批注锁定行为](../code-quality/annotating-locking-behavior.md)。  
  
- 驱动程序属性和其他特定于域的属性批注。  
  
  或者，可以对所有参数，以便在你的意图更明显，使其更方便地进行检查，进行了批注进行都批注。  
  
## <a name="related-resources"></a>相关资源  
 [代码分析团队博客](http://go.microsoft.com/fwlink/p/?LinkId=251197)  
  
## <a name="see-also"></a>请参阅  
 [使用 SAL 注释减少 C /C++代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [对函数参数和返回值进行批注](../code-quality/annotating-function-parameters-and-return-values.md)   
 [对函数行为进行批注](../code-quality/annotating-function-behavior.md)   
 [批注结构和类](../code-quality/annotating-structs-and-classes.md)   
 [对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)   
 [指定何时以及在何处应用批注](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)
