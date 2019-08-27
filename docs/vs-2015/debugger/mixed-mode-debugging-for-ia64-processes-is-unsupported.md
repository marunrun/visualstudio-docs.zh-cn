---
title: 不支持对 IA64 进程执行混合模式调试。 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_ia64
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 20bc1e38-049b-4388-87c4-936815d85b46
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c3cf7308b3302c682f32a2db9837f86cd0173260
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203287"
---
# <a name="mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>不支持对 IA64 进程执行混合模式调试。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 不支持对 IA64 进程中的托管代码和本机代码执行混合模式调试。 这意味着，当您进行调试时，无法从托管代码单步执行到本机代码，也无法从本机代码单步执行到托管代码。  
  
### <a name="workarounds"></a>问题解决  
  
- 在单独的调试会话中调试托管代码和本机代码。  
  
     –或者–  
  
     作为 32 位进程调试混合代码，如下面的过程所述。  
  
### <a name="to-change-the-platform-to-32-bit-visual-basic-or-c"></a>将平台更改为 32 位（Visual Basic 或 C#）  
  
1. 在“解决方案资源管理器”中，右键单击项目，然后在快捷菜单中单击“属性”   。  
  
2. 在属性页中，单击“编译”或“调试”选项卡   。  
  
3. 单击“平台”，然后从平台列表中选择“x86”  。  
  
     默认情况下，Visual Basic 和 C# 编译器默认生成要在任何 CPU 上运行的代码。 在 64 位计算机上，这些二进制代码作为 64 位进程运行。 若要在 32 位进程中运行，必须选择“Win32”而不是“AnyCPU”   。  
  
### <a name="to-change-the-platform-to-32-bit-cc"></a>将平台更改为 32 位 (C/C++)  
  
1. 在“解决方案资源管理器”中，右键单击项目，然后在快捷菜单中单击“属性”   。  
  
2. 在属性页中，单击“平台”，然后从平台列表中选择“Win32”   
  
## <a name="see-also"></a>请参阅  
 [调试 64 位应用程序](../debugger/debug-64-bit-applications.md)
