---
title: 错误：仅当使用 Microsoft .NET Framework 4 或更高版本时才支持对 x64 进程执行混合模式调试 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 67b9d1c737e4490195b209abca824b2d6d51176c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737601"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>错误：仅当使用 Microsoft .NET Framework 4 或更高版本时才支持对 x64 进程执行混合模式调试
若要调试64位进程中的混合本机代码和托管代码，你必须有 .NET Framework 版本4。 不支持对版本低于4的 .NET Framework 版本的64位进程进行混合模式调试。

### <a name="to-correct-this-error"></a>更正此错误

- 执行以下步骤之一：

  - 将 .NET Framework 升级到版本4。

  - 生成 32 位版本的应用程序以进行调试。

## <a name="see-also"></a>请参阅
- [Remote Debugging](../debugger/remote-debugging.md)