---
title: 混合代码和调用堆栈窗口中缺少的信息 |Microsoft Docs
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
ms.openlocfilehash: 025591ffea4d6746f87e5f1240cd226fa291d116
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905504"
---
# <a name="mixed-code-and-missing-information-in-the-call-stack-window"></a>“调用堆栈”窗口中的混合代码与丢失信息
由于托管代码和本机代码的调用堆栈之间存在差异，因此当代码类型混杂时，调试器无法始终显示完整的调用堆栈。 当本机代码调用托管的代码时，你可能会在“调用堆栈”窗口中注意到以下差异：

- 紧邻托管代码之上的本机框架可能从“调用堆栈”窗口中消失。 有关详细信息，请参阅[如何：在“调用堆栈”窗口中缺少本机框架时单步执行完托管代码](../debugger/how-to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-window.md)。

- 对于在调试器以外启动的混合模式应用程序，“调用堆栈”窗口可能只显示托管代码，而不显示任何本机框架。

  这两种情况都极为少见。 在多数对托管代码的本机调用中，都会正确显示调用堆栈。

## <a name="see-also"></a>请参阅
- [如何：使用“调用堆栈”窗口](../debugger/how-to-use-the-call-stack-window.md)