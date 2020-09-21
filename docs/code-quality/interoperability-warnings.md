---
title: 可移植性和互操作性警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Portablityrules
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis rules, interoperability rules, portability rules
- portability rules
- rules, portability
- interoperability rules
- rules, interoperability
ms.assetid: 95de6eb3-40c4-4063-9f59-25cb70e3b2b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8a456f4a24339b6cba5aeec2c9fe64ad3ee278b
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808595"
---
# <a name="portability-and-interoperability-rules"></a>可移植性和互操作性规则

可移植性规则支持跨不同平台的可移植性。 互操作性规则支持与 COM 客户端的交互。

## <a name="in-this-section"></a>本节内容

| 规则 | 描述 |
| - | - |
| [CA1401： P/Invoke 应不可见](../code-quality/ca1401.md) | 公共类型中的公共或受保护方法具有 System.Runtime.InteropServices.DllImportAttribute 特性 (也由 Visual Basic) 中的 Declare 关键字实现。 这些方法不能公开。 |
| [CA1416：验证平台兼容性](../code-quality/ca1416.md) | 在组件上使用平台相关的 Api 使代码在所有平台上都不再工作。 |
| [CA1417：不 `OutAttribute` 在 P/invoke 的字符串参数上使用](../code-quality/ca1417.md) | 如果字符串是暂存的字符串，则通过值传递的字符串参数与 `OutAttribute` 运行时的不稳定性。 |
