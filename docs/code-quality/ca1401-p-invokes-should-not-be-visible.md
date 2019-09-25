---
title: CA1401:P-Invokes 应该是不可见的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PInvokesShouldNotBeVisible
- CA1401
helpviewer_keywords:
- CA1401
- PInvokesShouldNotBeVisible
ms.assetid: 0f4d96c1-f9de-414e-b223-4dc7f691bee3
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d4a0a1c001407d947988497c422fdb8e88dd7c83
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234897"
---
# <a name="ca1401-pinvokes-should-not-be-visible"></a>CA1401:P/Invokes 应该是不可见的

|||
|-|-|
|TypeName|PInvokesShouldNotBeVisible|
|CheckId|CA1401|
|类别|Microsoft.Interoperability|
|重大更改|重大|

## <a name="cause"></a>原因
公共类型中的公共或受保护方法具有<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>特性（也在中`Declare` [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]由关键字实现）。

## <a name="rule-description"></a>规则说明
使用<xref:System.Runtime.InteropServices.DllImportAttribute>特性（或中`Declare` [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]使用关键字定义的方法）标记的方法使用平台调用服务来访问非托管代码。 这些方法不能公开。 通过使这些方法保持私有或内部，你可以通过允许调用方访问不能调用的非托管 Api 来确保你的库不能用于破坏安全性。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请更改该方法的访问级别。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例声明了违反此规则的方法。

[!code-vb[FxCop.Interoperability.DllImports#1](../code-quality/codesnippet/VisualBasic/ca1401-p-invokes-should-not-be-visible_1.vb)]
[!code-csharp[FxCop.Interoperability.DllImports#1](../code-quality/codesnippet/CSharp/ca1401-p-invokes-should-not-be-visible_1.cs)]