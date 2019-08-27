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
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: ba14fdbc23968fcaf10355f73517ab6cd54f8797
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142185"
---
# <a name="specifying-when-and-where-an-annotation-applies"></a>指定何时以及在何处应用批注
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

条件批注时，可能需要指定到分析器的其他批注。  例如，如果函数具有可以是同步还是异步的变量，将函数的行为，如下所示：在同步的情况下它始终会最终成功，但在异步情况下它报告错误如果它不能立即成功。 以同步方式调用该函数时，检查结果值提供到代码分析器的任何值，因为它将不返回。  但是，当以异步方式调用该函数并不检查函数结果，可能发生严重错误。 此示例说明了你可以在其中使用情况`_When_`批注 — 本文稍后所述，若要启用检查。  
  
## <a name="structural-annotations"></a>结构化批注  
 若要控制何时何地应用批注，请使用以下结构化批注。  
  
|批注|描述|  
|----------------|-----------------|  
|`_At_(expr, anno-list)`|`expr` 是生成左值的表达式。 中的批注`anno-list`应用于的对象，由名为`expr`。 对于在每个批注`anno-list`，`expr`如果批注解释在前提条件，而在后置条件如果批注被解释后置条件中解释在前提条件。|  
|`_At_buffer_(expr, iter, elem-count, anno-list)`|`expr` 是生成左值的表达式。 中的批注`anno-list`应用于的对象，由名为`expr`。 对于在每个批注`anno-list`，`expr`如果批注解释中不满足前提条件，而在后置条件如果批注被解释后置条件中解释在前提条件。<br /><br /> `iter` 范围限定为批注的变量的名称 (包括`anno-list`)。 `iter` 具有隐式类型`long`。 评估隐藏任何封闭作用域中具有相同名称的变量。<br /><br /> `elem-count` 是一个表达式的计算结果为整数。|  
|`_Group_(anno-list)`|中的批注`anno-list`均被视为具有适用于组批注应用于每个批注的任何限定符。|  
|`_When_(expr, anno-list)`|`expr` 一个表达式，可以转换为`bool`。 非零值时 (`true`) 中, 指定的批注`anno-list`被视为适用。<br /><br /> 默认情况下，在每个批注`anno-list`，`expr`被解释为使用输入的值，如果批注是前置条件，并且如果使用的输出值的批注是后置条件。 若要重写默认值，可以使用`_Old_`内部函数，当你的计算结果以指示应使用输入的值后置条件。 **注意：** 可能是因为使用启用不同的注释`_When_`如果可变值-例如， `*pLength`— 因为涉及的计算的结果`expr`中不满足前提条件可能不同于其计算结果后置条件中。|  
  
## <a name="see-also"></a>请参阅  
 [使用 SAL 注释减少 C /C++代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [了解 SAL](../code-quality/understanding-sal.md)   
 [对函数参数和返回值进行批注](../code-quality/annotating-function-parameters-and-return-values.md)   
 [对函数行为进行批注](../code-quality/annotating-function-behavior.md)   
 [批注结构和类](../code-quality/annotating-structs-and-classes.md)   
 [对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)   
 [内部函数](../code-quality/intrinsic-functions.md)   
 [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)
