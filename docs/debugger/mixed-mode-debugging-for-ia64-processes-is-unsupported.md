---
title: 不支持对 IA64 进程执行混合模式调试。 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_ia64
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 20bc1e38-049b-4388-87c4-936815d85b46
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c85c31cff5920ba3dc4b9356a1865d0db2323b2d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72731108"
---
# <a name="mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>不支持对 IA64 进程执行混合模式调试。
Visual Studio 不支持对 IA64 进程中的托管代码和本机代码执行混合模式调试。 这意味着，当您进行调试时，无法从托管代码单步执行到本机代码，也无法从本机代码单步执行到托管代码。

### <a name="workarounds"></a>问题解决

- 在单独的调试会话中调试托管代码和本机代码。

     \- 或 -

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
- [调试 64 位应用程序](../debugger/debug-64-bit-applications.md)