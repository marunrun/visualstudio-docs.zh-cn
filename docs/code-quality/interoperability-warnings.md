---
title: 可移植性和互操作性警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Portablityrules
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis warnings, interoperability warnings, portability warnings
- portability warnings
- warnings, portability
- interoperability warnings
- warnings, interoperability
ms.assetid: 95de6eb3-40c4-4063-9f59-25cb70e3b2b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 306c2477e6e5f731ed6dbf20b2cf4d03d4556467
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2020
ms.locfileid: "89509908"
---
# <a name="portability-and-interoperability-warnings"></a>可移植性和互操作性警告

可移植性警告支持跨不同平台的可移植性。 互操作性警告支持与 COM 客户端交互。

## <a name="in-this-section"></a>本节内容

| 规则 | 描述 |
| - | - |
| [CA1401： P/Invoke 应不可见](../code-quality/ca1401.md) | 公共类型中的公共或受保护方法具有 System.Runtime.InteropServices.DllImportAttribute 特性 (也由 Visual Basic) 中的 Declare 关键字实现。 这些方法不能公开。 |
| [CA1417：不 `OutAttribute` 在 P/invoke 的字符串参数上使用](../code-quality/ca1417.md) | 如果字符串是暂存的字符串，则通过值传递的字符串参数与 `OutAttribute` 运行时的不稳定性。 |