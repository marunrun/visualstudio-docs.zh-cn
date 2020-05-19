---
title: 错误：不支持对 IA64 进程执行混合模式调试 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.interop_unsupported_ia64
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0bddbb1572bd0258eae2052eb34dfa3d0d67a134
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737629"
---
# <a name="error-mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>错误：不支持对 IA64 进程执行混合模式调试
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 调试器不支持对基于 Itanium 的进程中的混合本机代码和托管代码进行调试。

### <a name="to-correct-this-error"></a>更正此错误

- 生成 32 位版本的应用程序以进行调试。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)