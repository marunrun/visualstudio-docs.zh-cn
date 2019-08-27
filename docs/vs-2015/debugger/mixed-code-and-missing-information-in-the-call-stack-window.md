---
title: 混合代码和调用堆栈窗口中缺少的信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- VB
- CSharp
- C++
helpviewer_keywords:
- managed code, stepping
- Call Stack window, mixed-mode debugging
- Call Stack window, troubleshooting
- native frames
- managed call stacks
- mixed-mode debugging, call stack
- stepping, out of managed code
ms.assetid: dd628427-e8d6-4fc2-b524-9d6393ea5376
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3995e14379fa4bd3ebd5cc276613c288b4437d35
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193275"
---
# <a name="mixed-code-and-missing-information-in-the-call-stack-window"></a>“调用堆栈”窗口中的混合代码与丢失信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

由于托管代码和本机代码的调用堆栈之间存在差异，因此当代码类型混杂时，调试器无法始终显示完整的调用堆栈。 当本机代码调用托管的代码时，你可能会在“调用堆栈”窗口中注意到以下差异：   
  
- 紧邻托管代码之上的本机框架可能从“调用堆栈”窗口中消失  。 有关详细信息，请参阅[如何：在“调用堆栈”窗口中缺少本机框架时单步执行完托管代码](../debugger/how-to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-window.md)。  
  
- 对于在调试器以外启动的混合模式应用程序，“调用堆栈”窗口可能只显示托管代码，而不显示任何本机框架  。  
  
  这两种情况都极为少见。 在多数对托管代码的本机调用中，都会正确显示调用堆栈。  
  
## <a name="see-also"></a>请参阅  
 [如何：使用“调用堆栈”窗口](../debugger/how-to-use-the-call-stack-window.md)
