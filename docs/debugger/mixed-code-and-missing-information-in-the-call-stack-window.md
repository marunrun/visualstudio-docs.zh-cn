---
title: "\"调用堆栈\" 窗口中的混合代码和缺失信息 |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: troubleshooting
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- managed code, stepping
- Call Stack window, mixed-mode debugging
- Call Stack window, troubleshooting
- native frames
- managed call stacks
- mixed-mode debugging, call stack
- stepping, out of managed code
ms.assetid: dd628427-e8d6-4fc2-b524-9d6393ea5376
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a314634766618340e3fb69052bc896cae700d4b4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72731144"
---
# <a name="mixed-code-and-missing-information-in-the-call-stack-window"></a>“调用堆栈”窗口中的混合代码与丢失信息
由于托管代码和本机代码的调用堆栈之间存在差异，因此对于混合的代码类型，调试器不能始终显示完整的调用堆栈。 本机代码调用托管代码时，可能会注意到“调用堆栈”窗口中的内容与实际情况存在如下差异：

- 紧邻托管代码之上的本机框架可能从“调用堆栈”窗口中消失。 有关详细信息，请参阅[如何：在 "调用堆栈" 窗口中缺少本机框架时跳出托管代码](../debugger/how-to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-window.md)。

- 对于在调试器以外启动的混合模式应用程序，“调用堆栈”窗口可能只显示托管代码，而不显示任何本机框架。

  这两种情况都极为少见。 在多数对托管代码的本机调用中，都会正确显示调用堆栈。

## <a name="see-also"></a>请参阅
- [如何：使用“调用堆栈”窗口](../debugger/how-to-use-the-call-stack-window.md)