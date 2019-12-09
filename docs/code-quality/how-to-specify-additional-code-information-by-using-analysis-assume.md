---
title: Use _Analysis_assume for code analysis hints
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _Analysis_assume
helpviewer_keywords:
- _Analysis_assume
ms.assetid: 51205d97-4084-4cf4-a5ed-3eeaf67deb1b
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: 9933a013ed4f2df0978fb66e3aff87b4cdc024f9
ms.sourcegitcommit: c6af923c1f485959d751b23ab3f03541013fc4a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2019
ms.locfileid: "73925964"
---
# <a name="how-to-specify-additional-code-information-by-using-_analysis_assume"></a>How to: Specify Additional Code Information by Using _Analysis_assume

You can provide hints to the code analysis tool for C/C++ code that will help the analysis process and reduce warnings. To provide additional information, use the following function:

`_Analysis_assume(`  `expr`  `)`

`expr` - any expression that is assumed to evaluate to true.

The code analysis tool assumes that the condition represented by the expression is true at the point where the function appears and remains true until expression is altered, for example, by assignment to a variable.

> [!NOTE]
> `_Analysis_assume` does not impact code optimization. Outside the code analysis tool, `_Analysis_assume` is defined as a no-op.

## <a name="example"></a>示例

The following code uses `_Analysis_assume` to correct the code analysis warning [C6388](../code-quality/c6388.md):

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
    _Analysis_assume(pc == NULL);
    f(pc);
}
```

## <a name="see-also"></a>请参阅

- [__assume](/cpp/intrinsics/assume)
