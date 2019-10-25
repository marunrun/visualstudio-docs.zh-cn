---
title: 错误：仅当使用 Microsoft .NET Framework 2.0 或更高版本时才支持混合模式调试 | Microsoft Docs
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
ms.openlocfilehash: c85dac85146c59d8aeba9f9cf85351b5bc17a81c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737614"
---
# <a name="error-mixed-mode-debugging-is-supported-only-when-using-microsoft-net-framework-20-or-greater"></a>错误：仅当使用 Microsoft .NET Framework 2.0 或更高版本时，才支持混合模式调试
若要调试混合的本机代码和托管代码，则必须具有 .NET Framework 版本2.0、3.0。 3.5 或 4 版。 不支持 .NET Framework 的早期版本进行混合模式调试。

### <a name="to-correct-this-error"></a>更正此错误

- 将 .NET Framework 升级到版本2.0、3.0、3.5 或4.0。

## <a name="see-also"></a>请参阅
- [Remote Debugging](../debugger/remote-debugging.md)