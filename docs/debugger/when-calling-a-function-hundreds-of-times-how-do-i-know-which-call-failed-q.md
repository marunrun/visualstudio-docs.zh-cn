---
title: 多次调用函数时查找调用失败
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.functions
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- conditional breakpoints
- errors [debugger], function calls
- breakpoints, troubleshooting
- errors [debugger], finding which function call failed
- failures
- location breakpoint call failures
- errors [Visual Studio], function calls
- hit counts
- function calls, failure
- functions [debugger]
- Skip Count
ms.assetid: 66cfac86-f5be-4d3a-9329-d44cd74bc586
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: de3d186b7800efc3e807e3f775b48d91b44072b4
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810479"
---
# <a name="when-calling-a-function-hundreds-of-times-how-do-i-know-which-call-failed"></a>当一个函数被调用数百次时，如何确定哪次调用失败了？
## <a name="problem-description"></a>问题描述
 程序在调用某函数（如 `CnvtV`）时失败。 失败以前该程序可能已调用了该函数数百次。 如果我在 `CnvtV` 上设置一个位置断点，程序在每次调用该函数时都停止，而我不希望这样。 我不知道什么条件导致调用失败，所以无法设置条件断点。 我该怎么办？

## <a name="solution"></a>解决方案
 在函数上设置断点时可以将“命中次数”字段设置为一个大到永远无法达到的值。 在这种情况中，由于你确信函数 `CnvtV` 被调用了数百次，所以将“命中次数”设置为 1000 或更高。 然后运行程序，等待调用失败。 程序失败后，打开“断点”窗口并查看断点列表。 将显示您在 `CnvtV` 上设置的断点，其后跟着命中次数和剩余迭代次数：

```cpp
CnvtV(int) (no condition) when hit count is equal to 1000 (currently 101)
```

 现在您知道函数在第 101 次调用时失败。 如果重置断点，将命中次数设置为 101，然后再次运行程序，程序将在导致 `CnvtV` 调用失败的位置停止所有该调用。

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [设置断点](/previous-versions/ktf38f66(v=vs.100))
- [调试本机代码](../debugger/debugging-native-code.md)