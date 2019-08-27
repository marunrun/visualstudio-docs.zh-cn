---
title: CA2004:移除对 GC.KeepAlive 的调用
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
helpviewer_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
ms.assetid: bc543b5b-23eb-4b45-abc2-9325cd254ac2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a716da8eb0fb1b741c302ed32408e63a4933567b
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921136"
---
# <a name="ca2004-remove-calls-to-gckeepalive"></a>CA2004:移除对 GC.KeepAlive 的调用

|||
|-|-|
|TypeName|RemoveCallsToGCKeepAlive|
|CheckId|CA2004|
|类别|Microsoft.Reliability|
|是否重大更改|不间断|

## <a name="cause"></a>原因
类使用`SafeHandle`但仍包含对`GC.KeepAlive`的调用。

## <a name="rule-description"></a>规则说明
如果要转换为`SafeHandle`用法, 请删除对`GC.KeepAlive` (object) 的所有调用。 在这种情况下, 类不应调用`GC.KeepAlive`, 前提是它们没有终结器, 而是`SafeHandle`依赖于完成它们的操作系统句柄。  尽管对的调用`GC.KeepAlive`的开销可能会因为性能的衡量而忽略不计, 但感觉到`GC.KeepAlive`对的调用是必要的或足以解决可能不再存在的生存期问题, 这会使代码更难以实现.

## <a name="how-to-fix-violations"></a>如何解决冲突
删除对`GC.KeepAlive`的调用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
仅当在技术上不能转换为`SafeHandle`类中的使用情况时, 才可以禁止显示此警告。