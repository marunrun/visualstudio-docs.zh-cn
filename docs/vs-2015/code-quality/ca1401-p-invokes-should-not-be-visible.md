---
title: CA1401： P-调用不应是可见的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PInvokesShouldNotBeVisible
- CA1401
helpviewer_keywords:
- CA1401
- PInvokesShouldNotBeVisible
ms.assetid: 0f4d96c1-f9de-414e-b223-4dc7f691bee3
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f3f867f14f7a2eca4482f1f8d5fb48149f02f43f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661360"
---
# <a name="ca1401-pinvokes-should-not-be-visible"></a>CA1401：P/Invokes 应该是不可见的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PInvokesShouldNotBeVisible|
|CheckId|CA1401|
|类别|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共类型中的公共或受保护方法具有 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 特性（还由 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中的 `Declare` 关键字实现）。

## <a name="rule-description"></a>规则说明
 使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 特性标记的方法（或在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中使用 `Declare` 关键字定义的方法）使用平台调用服务来访问非托管代码。 这些方法不能公开。 通过使这些方法保持私有或内部，你可以通过允许调用方访问不能调用的非托管 Api 来确保你的库不能用于破坏安全性。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请更改该方法的访问级别。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例声明了违反此规则的方法。

 [!code-csharp[FxCop.Interoperability.DllImports#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DllImports/cs/FxCop.Interoperability.DllImports.cs#1)]
 [!code-vb[FxCop.Interoperability.DllImports#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DllImports/vb/FxCop.Interoperability.DllImports.vb#1)]
