---
title: CA1011：考虑将基类型作为参数传递 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ConsiderPassingBaseTypesAsParameters
- CA1011
helpviewer_keywords:
- CA1011
- ConsiderPassingBaseTypesAsParameters
ms.assetid: ce1e1241-dcf4-419b-9363-1d5bc4989279
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 3968d81e8ee18b4b0a56bed50f7aa1f121e1c074
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663245"
---
# <a name="ca1011-consider-passing-base-types-as-parameters"></a>CA1011：考虑将基类型作为参数传递
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ConsiderPassingBaseTypesAsParameters|
|CheckId|CA1011|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 方法声明包含一个派生类型的形参，而方法仅调用该参数的基类型的成员。

## <a name="rule-description"></a>规则说明
 在方法声明中将基类型指定为参数时，可以将派生自基类型的任何类型作为相应的参数传递给方法。 在方法体中使用参数时，执行的特定方法取决于参数的类型。 如果派生类型提供的其他功能不是必需的，则使用基类型可以更广泛使用该方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将参数的类型更改为其基类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 可以安全地禁止显示此规则发出的警告

- 如果方法需要由派生类型提供的特定功能，

   \- 或 -

- 若要强制只将派生类型或派生程度更高的类型传递给方法。

  在这些情况下，由于编译器和运行时提供的强类型检查，代码将更可靠。

## <a name="example"></a>示例
 下面的示例演示一个 `ManipulateFileStream` 方法，该方法只能与违反此规则的 <xref:System.IO.FileStream> 对象一起使用。 第二种方法（`ManipulateAnyStream`）通过使用 <xref:System.IO.Stream> 替换 <xref:System.IO.FileStream> 参数来满足规则。

 [!code-cpp[FxCop.Design.ConsiderPassingBaseTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ConsiderPassingBaseTypes/cpp/FxCop.Design.ConsiderPassingBaseTypes.cpp#1)]
 [!code-csharp[FxCop.Design.ConsiderPassingBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ConsiderPassingBaseTypes/cs/FxCop.Design.ConsiderPassingBaseTypes.cs#1)]
 [!code-vb[FxCop.Design.ConsiderPassingBaseTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ConsiderPassingBaseTypes/vb/FxCop.Design.ConsiderPassingBaseTypes.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1059：成员不应公开某些具体类型](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md)
