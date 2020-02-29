---
title: 可移植性警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.PortabilityRules
helpviewer_keywords:
- portability warnings
- managed code analysis warnings, portability warnings
- warnings, portability
ms.assetid: 902e859a-2153-4970-baaa-8a5b4a11806f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f48cef7ffaf08fc26566fdd04bee15a3e3e1b85f
ms.sourcegitcommit: 1efb6b219ade7c35068b79fbdc573a8771ac608d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78167568"
---
# <a name="portability-warnings"></a>可移植性警告
可移植性警告支持跨不同操作系统的可移植性。

## <a name="in-this-section"></a>本节内容

|规则|说明|
|----------|-----------------|
|[CA1900：值类型字段应为可移植字段](../code-quality/ca1900.md)|此规则检查在被封送到64位操作系统上的非托管代码时，使用显式布局特性声明的结构是否会正确对齐。|
|[CA1901：P/Invoke 声明应为可移植声明](../code-quality/ca1901.md)|此规则计算每个参数的大小和 P/Invoke 的返回值，并验证在将其封送到32位和64位操作系统上的非托管代码时，其大小是否正确。|
|[CA1903：仅使用目标框架中的 API](../code-quality/ca1903.md)|一个成员或类型使用了某个 Service Pack 中引入的成员或类型，该 Service Pack 没有与项目的目标框架一起包括。|
