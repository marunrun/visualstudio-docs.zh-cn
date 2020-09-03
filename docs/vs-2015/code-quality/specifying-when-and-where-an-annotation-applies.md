---
title: 指定何时以及在何处应用批注 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Group_
- _At_
- _When_
- _At_buffer_
ms.assetid: 8e4f4f9c-5dfa-4835-87df-ecd1698fc650
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 1eb32aa7d87da75ebf37b27aa1d425adb85f8c9b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "77278451"
---
# <a name="specifying-when-and-where-an-annotation-applies"></a>指定何时以及在何处应用批注
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果批注是有条件的，则可能需要其他批注来指定分析器。  例如，如果某个函数具有可同步或异步的变量，则该函数的行为如下所示：在同步的情况下，它始终会成功，但在异步情况下，它会报告错误（如果它无法立即成功）。 同步调用函数时，检查结果值不会为代码分析器提供任何值，因为它不返回。  但是，如果异步调用函数，但未检查函数结果，则可能出现严重错误。 此示例演示了一种情况，在这种情况下，你可以使用 `_When_` 批注（如本文稍后所述）启用检查。  
  
## <a name="structural-annotations"></a>结构化批注  
 若要控制批注的应用时间和位置，请使用以下结构注释。  
  
|Annotation|说明|  
|----------------|-----------------|  
|`_At_(expr, anno-list)`|`expr` 生成左值的表达式。 中的批注 `anno-list` 应用于由命名的对象 `expr` 。 对于中的每个批注 `anno-list` ， `expr` 如果批注在前置条件下被解释，则在前置条件中进行解释; 如果在后置条件下，批注则在 post 条件下进行解释。|  
|`_At_buffer_(expr, iter, elem-count, anno-list)`|`expr` 生成左值的表达式。 中的批注 `anno-list` 应用于由命名的对象 `expr` 。 对于中的每个批注 `anno-list` ， `expr` 如果注释在前置条件中进行解释，则在前置条件中进行解释; 如果在后置条件下，批注则在 post 条件下进行解释。<br /><br /> `iter` 属于注释 (包含) 的变量的名称 `anno-list` 。 `iter` 具有隐式类型 `long` 。 任何封闭范围中具有相同名称的变量在计算中都是隐藏的。<br /><br /> `elem-count` 计算结果为整数的表达式。|  
|`_Group_(anno-list)`|中的批注 `anno-list` 全都被视为具有应用于每个批注的组批注的任何限定符。|  
|`_When_(expr, anno-list)`|`expr` 可转换为的表达式 `bool` 。 如果 () 为非零 `true` ，则在中指定的批注将被 `anno-list` 视为适用。<br /><br /> 默认情况下，对于中的每个批注， `anno-list` `expr` 如果批注是前置条件，则将其解释为使用输入值; 如果批注是后置条件，则将其解释为使用输出值。 若要重写默认值，您可以 `_Old_` 在评估 post 条件时使用内部，以指示应使用输入值。 **注意：**  如果使用可变值（例如），则可能会启用不同的批注， `_When_` `*pLength` 因为 `expr` 在前置条件中，在前置条件中，计算结果可能不同于其计算结果。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 SAL 注释减少 C/c + + 代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [了解 SAL](../code-quality/understanding-sal.md)   
 [注释函数参数和返回值](../code-quality/annotating-function-parameters-and-return-values.md)   
 [注释函数行为](../code-quality/annotating-function-behavior.md)   
 [批注结构和类](../code-quality/annotating-structs-and-classes.md)   
 [批注锁定行为](../code-quality/annotating-locking-behavior.md)   
 [内部函数](../code-quality/intrinsic-functions.md)   
 [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)
