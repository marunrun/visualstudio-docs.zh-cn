---
title: 内部函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _String_length_
- _Param_
- _Curr_
- _Old_
- _Nullterm_length_
- _Inexpressible_
ms.assetid: adf29f8c-89fd-4a5e-9804-35ac83e1c457
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: a0a6cd31cbc8cf73cfa2c7e9ee7c096fa56799b9
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77277964"
---
# <a name="intrinsic-functions"></a>内部函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

SAL 中的表达式可以是 C/C++表达式，前提是它是一个不具有副作用的表达式，例如 + +、--, 和函数调用都在此上下文中有副作用。  但是，SAL 提供一些类似函数的对象和一些可用于 SAL 表达式的保留符号。 这些*函数称为内部函数*。  
  
## <a name="general-purpose"></a>通用  
 以下内部函数注释提供了用于 SAL 的常规实用工具。  
  
|Annotation|说明|  
|----------------|-----------------|  
|`_Curr_`|当前正在进行批注的对象的同义词。  当使用 `_At_` 批注时，`_Curr_` 与 `_At_`的第一个参数相同。  否则，它是批注在词法上关联的参数或整个函数/返回值。|  
|`_Inexpressible_(expr)`|表示缓冲区的大小太复杂，无法通过使用批注表达式来表示，例如，通过扫描输入数据集并对选定成员进行计数来计算。|  
|`_Nullterm_length_(param)`|`param` 是缓冲区中的元素数目，但不包括 null 终止符。 它可以应用于非聚合非 void 类型的任何缓冲区。|  
|`_Old_(expr)`|当在前置条件中进行计算时，`_Old_` 返回输入值 `expr`。  当在后置条件中进行计算时，它将返回值 `expr`，因为它会在前置条件中进行计算。|  
|`_Param_(n)`|函数的 `n`第一个参数，从1到 `n`，`n` 是一个文本整数常量。 如果参数名为，则此批注与按名称访问参数相同。 **注意：** `n` 可以引用省略号定义的位置参数，也可以在未使用名称的函数原型中使用。|  
|`return`|可以在 SALC++表达式中使用 C/reserved 关键字 `return` 来指示函数的返回值。  该值仅在 post 状态中可用;在 pre 状态中使用它是一个语法错误。|  
  
## <a name="string-specific"></a>特定于字符串  
 以下内部函数批注允许对字符串进行操作。 所有这四个函数都具有相同的用途：返回在 null 终止符之前找到的类型的元素数。 不同之处在于引用的元素中的数据类型。 请注意，如果想要指定不由字符组成的以 null 结尾的缓冲区的长度，请使用上一节中的 `_Nullterm_length_(param)` 注释。  
  
|Annotation|说明|  
|----------------|-----------------|  
|`_String_length_(param)`|`param` 是字符串中的元素数，最大为，但不包括 null 终止符。 此批注是为字符字符串类型保留的。|  
|`strlen(param)`|`param` 是字符串中的元素数，最大为，但不包括 null 终止符。 此批注保留用于字符数组，类似于 C 运行时函数[strlen （）](https://msdn.microsoft.com/library/16462f2a-1e0f-4eb3-be55-bf1c83f374c2)。|  
|`wcslen(param)`|`param` 是字符串中的元素数（但不包括）为 null 终止符。 此批注保留用于宽字符数组，类似于 C 运行时函数[wcslen （）](https://msdn.microsoft.com/library/16462f2a-1e0f-4eb3-be55-bf1c83f374c2)。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 SAL 注释减少 C/C++代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [了解 SAL](../code-quality/understanding-sal.md)   
 [批注函数参数和返回值](../code-quality/annotating-function-parameters-and-return-values.md)   
 [批注函数行为](../code-quality/annotating-function-behavior.md)   
 [批注结构和类](../code-quality/annotating-structs-and-classes.md)   
 [批注锁定行为](../code-quality/annotating-locking-behavior.md)   
 [指定何时以及在何处应用批注](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)
