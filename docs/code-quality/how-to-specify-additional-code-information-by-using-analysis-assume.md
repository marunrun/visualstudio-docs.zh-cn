---
title: 使用 _Analysis_assume 进行代码分析提示
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _Analysis_assume
helpviewer_keywords:
- _Analysis_assume
ms.assetid: 51205d97-4084-4cf4-a5ed-3eeaf67deb1b
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 1d3c80f0780dcd577356de69944dcc76cca7133c
ms.sourcegitcommit: ab06cde69d862440b4277bcd9bf02e7b50593a1b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67132121"
---
# <a name="how-to-specify-additional-code-information-by-using-analysisassume"></a>如何：使用 _Analysis_assume 指定其他代码信息

您可以对代码分析工具的提示，对于 C /C++代码，可以帮助分析处理并减少警告。 若要提供的其他信息，请使用以下函数：

`_Analysis_assume(`  `expr`  `)`

`expr` -假定为计算结果为 true 的任何表达式。

代码分析工具假设由表达式表示的条件是在其中该函数将显示，并将保持为 true，直到表达式更改，例如，通过对变量赋值的点，则返回 true。

> [!NOTE]
> `_Analysis_assume` 不会影响代码优化。 外部代码分析工具，`_Analysis_assume`定义为执行任何操作。

## <a name="example"></a>示例

下面的代码使用`_Analysis_assume`若要更正代码分析警告[C6388](../code-quality/c6388.md):

```cpp
#include<windows.h>
#include<codeanalysis\sourceannotations.h>

using namespace vc_attributes;

//requires pc to be null
void f([Pre(Null=Yes)] char* pc);

// calls free and sets ch to null
void FreeAndNull(char** ch);

void test()
{
    char pc = (char)malloc(5);
    FreeAndNull(&pc);
    __analysis_assume(pc == NULL);
    f(pc);
}
```

## <a name="see-also"></a>请参阅

- [__assume](/cpp/intrinsics/assume)
