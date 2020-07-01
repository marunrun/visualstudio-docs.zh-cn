---
title: CA2208：正确实例化参数异常 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2208
- InstantiateArgumentExceptionsCorrectly
helpviewer_keywords:
- InstantiateArgumentExceptionsCorrectly
- CA2208
ms.assetid: e2a48939-d9fa-478c-b2f9-3bdbce07dff7
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6a63ebb7f3946926864c4dd882c281b5dcd7c6c5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535832"
---
# <a name="ca2208-instantiate-argument-exceptions-correctly"></a>CA2208:正确实例化参数异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|InstantiateArgumentExceptionsCorrectly|
|CheckId|CA2208|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 可能的原因包括以下情况：

- 调用了异常类型的默认（无参数）构造函数，或派生自 [ArgumentException] （<!-- TODO: review code entity reference <xref:assetId:///System.ArgumentException?qualifyHint=True&amp;autoUpgrade=True>  -->).

- 将不正确的字符串自变量传递给异常类型的参数化构造函数，或从 [ArgumentException] 派生。(<!-- TODO: review code entity reference <xref:assetId:///System.ArgumentException.?qualifyHint=True&amp;autoUpgrade=True>  -->)

## <a name="rule-description"></a>规则描述
 不是调用默认构造函数，而是调用允许提供更有意义的异常消息的构造函数重载之一。 异常消息应面向开发人员，并清楚地说明错误情况以及如何纠正或避免异常。

 及其派生类型的一个和两个字符串构造函数的签名与 <xref:System.ArgumentException> `message` 和参数不一致 `paramName` 。 请确保用正确的字符串参数调用这些构造函数。 签名如下所示：

 <xref:System.ArgumentException>（string `message` ）

 <xref:System.ArgumentException>（string `message` ，string `paramName` ）

 <xref:System.ArgumentNullException>（string `paramName` ）

 <xref:System.ArgumentNullException>（string `paramName` ，string `message` ）

 <xref:System.ArgumentOutOfRangeException>（string `paramName` ）

 <xref:System.ArgumentOutOfRangeException>（string `paramName` ，string `message` ）

 <xref:System.DuplicateWaitObjectException>（string `parameterName` ）

 <xref:System.DuplicateWaitObjectException>（string `parameterName` ，string `message` ）

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请调用使用消息的构造函数和/或参数名，并确保参数对于调用的类型是正确的 <xref:System.ArgumentException> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当使用正确的字符串参数调用参数化的构造函数时，才可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示一个构造函数，该构造函数错误地实例化 System.argumentnullexception 类型的实例。

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cpp/FxCop.Usage.InheritedPublic.cpp#1)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cs/FxCop.Usage.InheritedPublic.cs#1)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/vb/FxCop.Usage.InstantiateArgumentExceptionsCorrectly.vb#1)]

## <a name="example"></a>示例
 下面的示例通过切换构造函数参数来修复上述冲突。

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cpp/FxCop.Usage.InheritedPublic.cpp#2)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cs/FxCop.Usage.InheritedPublic.cs#2)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/vb/FxCop.Usage.InstantiateArgumentExceptionsCorrectly.vb#2)]
