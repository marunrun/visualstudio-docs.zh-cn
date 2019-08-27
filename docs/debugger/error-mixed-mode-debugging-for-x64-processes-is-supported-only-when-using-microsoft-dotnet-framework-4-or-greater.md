---
title: 错误：混合模式调试支持对 x64 进程是仅当使用 Microsoft.NET Framework 4 或更高版本 |Microsoft Docs
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
ms.openlocfilehash: 9ef0daf5fd28bd829edcdce412839b03ed8347bf
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66745442"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>错误：仅当使用 Microsoft .NET Framework 4 或更高版本时才支持对 x64 进程执行混合模式调试
若要调试 64 位进程中的混合本机和托管代码，必须具有.NET Framework 版本 4。 不支持混合模式调试的.NET Framework 版本 4 之前的 64 位进程。

### <a name="to-correct-this-error"></a>更正此错误

- 执行以下步骤之一：

  - 升级到版本 4 的.NET Framework。

  - 生成 32 位版本的应用程序以进行调试。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)