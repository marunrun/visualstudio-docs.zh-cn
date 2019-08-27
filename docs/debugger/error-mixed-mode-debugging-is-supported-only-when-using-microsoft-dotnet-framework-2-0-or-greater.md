---
title: 错误：仅在使用 Microsoft.NET Framework 2.0 或更高版本支持混合的模式调试 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.interop_unsupported_to_old
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
ms.openlocfilehash: 0fd30fb1b181224b61b96670553ef5aa6ff0f721
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66745284"
---
# <a name="error-mixed-mode-debugging-is-supported-only-when-using-microsoft-net-framework-20-or-greater"></a>错误：仅当使用 Microsoft .NET Framework 2.0 或更高版本时，才支持混合模式调试
若要调试混合本机和托管代码，必须具有.NET Framework 版本 2.0，3.0。 3.5 或 4 版。 不支持混合模式调试与早期版本的.NET Framework。

### <a name="to-correct-this-error"></a>更正此错误

- 升级到版本 2.0、 3.0、 3.5 或 4.0.NET Framework。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)