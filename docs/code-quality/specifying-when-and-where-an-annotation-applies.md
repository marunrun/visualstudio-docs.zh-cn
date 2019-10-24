---
title: 指定何时以及在何处应用批注
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _Group_
- _At_
- _When_
- _At_buffer_
ms.assetid: 8e4f4f9c-5dfa-4835-87df-ecd1698fc650
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: 8ccf20ab4348a8abed4b052f512477c8b2a8cd0b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745898"
---
# <a name="specifying-when-and-where-an-annotation-applies"></a>指定何时以及在何处应用批注
如果批注是有条件的，则可能需要其他批注来指定分析器。  例如，如果某个函数具有可同步或异步的变量，则该函数的行为如下所示：在同步的情况下，它始终会成功，但在异步情况下，它会报告错误（如果它无法立即成功）。 同步调用函数时，检查结果值不会为代码分析器提供任何值，因为它不返回。  但是，如果异步调用函数，但未检查函数结果，则可能出现严重错误。 此示例演示了一种情况，在这种情况下，你可以使用 `_When_` 注释（如本文稍后所述）启用检查。

## <a name="structural-annotations"></a>结构化批注
若要控制批注的应用时间和位置，请使用以下结构注释。

|批注|描述|
|----------------|-----------------|
|`_At_(expr, anno-list)`|`expr` 是产生左值的表达式。 @No__t_0 中的批注应用于 `expr` 命名的对象。 对于 `anno-list` 中的每个批注，如果批注在前置条件下进行解释，则在前置条件下解释 `expr`，如果在后置条件下，则在 post 条件下解释为。|
|`_At_buffer_(expr, iter, elem-count, anno-list)`|`expr` 是产生左值的表达式。 @No__t_0 中的批注应用于 `expr` 命名的对象。 对于 `anno-list` 中的每个批注，如果注释在前置条件下进行解释，则在前置条件下解释 `expr`，如果在后置条件下，批注则在 post 条件中进行解释。<br /><br /> `iter` 是指作为批注范围（包含 `anno-list`）的变量的名称。 `iter` 具有 `long` 的隐式类型。 任何封闭范围中具有相同名称的变量在计算中都是隐藏的。<br /><br /> `elem-count` 是计算结果为整数的表达式。|
|`_Group_(anno-list)`|@No__t_0 中的批注全都被视为具有应用于每个批注的组批注的任何限定符。|
|`_When_(expr, anno-list)`|`expr` 是可转换为 `bool` 的表达式。 如果为非零（`true`），则将 `anno-list` 中指定的批注视为适用。<br /><br /> 默认情况下，对于 `anno-list` 中的每个批注，如果批注是前置条件，则 `expr` 被解释为使用输入值; 如果批注是后置条件，则将其解释为使用输出值。 若要重写默认值，则在评估 post 条件时，可以使用 `_Old_` 内部，以指示应使用输入值。 **注意：** 如果使用 `_When_` （例如，`*pLength`），则可能会启用不同的批注，因为在前置条件中，在前置条件下，`expr` 计算得出的结果可能与其在后置条件中的计算结果不同。|

## <a name="see-also"></a>请参阅

- [使用 SAL 批注以减少 C/C++ 代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [了解 SAL](../code-quality/understanding-sal.md)
- [对函数参数和返回值进行批注](../code-quality/annotating-function-parameters-and-return-values.md)
- [对函数行为进行批注](../code-quality/annotating-function-behavior.md)
- [批注结构和类](../code-quality/annotating-structs-and-classes.md)
- [对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)
- [内部函数](../code-quality/intrinsic-functions.md)
- [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)
