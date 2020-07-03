---
title: 错误 - 仅当使用 Microsoft .NET Framework 4 或更高版本时才支持对 x64 进程执行混合模式调试 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
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
ms.openlocfilehash: 9f30fe9b729df84506f6717e5fd895297390dea6
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460632"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>错误：仅当使用 Microsoft .NET Framework 4 或更高版本时才支持对 x64 进程执行混合模式调试
若要调试 64 位进程中的混合本机代码和托管代码，你必须安装了 .NET Framework 版本 4。 低于 4 的 .NET Framework 版本不支持对 64 位进程进行混合模式调试。

### <a name="to-correct-this-error"></a>更正此错误

- 执行以下步骤之一：

  - 将 .NET Framework 升级到版本 4。

  - 生成 32 位版本的应用程序以进行调试。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)