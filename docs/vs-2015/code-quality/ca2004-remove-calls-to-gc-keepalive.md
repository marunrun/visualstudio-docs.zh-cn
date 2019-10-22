---
title: CA2004：删除对 GC 的调用。KeepAlive |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
helpviewer_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
ms.assetid: bc543b5b-23eb-4b45-abc2-9325cd254ac2
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e34a8e7d4860a599155554410e13df5a6eb3bfe1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672497"
---
# <a name="ca2004-remove-calls-to-gckeepalive"></a>CA2004：移除对 GC.KeepAlive 的调用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|RemoveCallsToGCKeepAlive|
|CheckId|CA2004|
|类别|Microsoft 可靠性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类使用 `SafeHandle` 但仍包含对 `GC.KeepAlive` 的调用。

## <a name="rule-description"></a>规则说明
 如果要转换为 `SafeHandle` 用法，请删除对 `GC.KeepAlive` （对象）的所有调用。 在这种情况下，类不必调用 `GC.KeepAlive`，假设它们没有终结器，但依赖于 `SafeHandle` 来完成它们的操作系统句柄。  尽管对 `GC.KeepAlive` 的调用的成本可能会从性能上得出不计，但从性能角度来看，对 `GC.KeepAlive` 的调用很有必要或足以解决可能不再存在的生存期问题，从而使代码更难以维护。

## <a name="how-to-fix-violations"></a>如何解决冲突
 删除对 `GC.KeepAlive` 的调用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当在技术上不正确时才可以禁止显示此警告，以将其转换为类中 `SafeHandle` 使用。
