---
title: CA1052：应密封静态容器类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldBeSealed
- CA1052
helpviewer_keywords:
- CA1052
- StaticHolderTypesShouldBeSealed
ms.assetid: 51a3165d-781e-4a55-aa0d-ea25fee7d4f2
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 14231cc4dcde5aed5cabc2d8a6172a002c0ba6bf
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539745"
---
# <a name="ca1052-static-holder-types-should-be-sealed"></a>CA1052:应密封静态容器类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|StaticHolderTypesShouldBeSealed|
|CheckId|CA1052|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型仅包含静态成员，并且不使用[sealed](https://msdn.microsoft.com/library/8e4ed5d3-10be-47db-9488-0da2008e6f3f) （[NotInheritable](https://msdn.microsoft.com/library/5c4da7c9-9562-4653-a947-1972e992f9f9)）修饰符进行声明。

## <a name="rule-description"></a>规则描述
 此规则假定只包含静态成员的类型不是被继承的，因为该类型不提供可在派生类型中重写的任何功能。 未计划继承的类型应该用 `sealed` 修饰符进行标记，以便禁止其作为基类型使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将类型标记为 `sealed` 。 如果目标是 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 2.0 或更早版本，则更好的方法是将类型标记为 `static` 。 通过这种方式，您就不必声明私有构造函数来阻止创建类。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当类型设计为继承时，禁止显示此规则发出的警告。 缺少 `sealed` 修饰符表明类型可用作基类型。

## <a name="example-of-a-violation"></a>冲突示例

### <a name="description"></a>描述
 下面的示例演示违反规则的类型。

### <a name="code"></a>代码
 [!code-cpp[FxCop.Design.StaticMembers#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembers/cpp/FxCop.Design.StaticMembers.cpp#1)]
 [!code-csharp[FxCop.Design.StaticMembers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembers/cs/FxCop.Design.StaticMembers.cs#1)]
 [!code-vb[FxCop.Design.StaticMembers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembers/vb/FxCop.Design.StaticMembers.vb#1)]

## <a name="fix-with-the-static-modifier"></a>用 Static 修饰符修复

### <a name="description"></a>描述
 下面的示例演示如何通过使用修饰符标记类型来修复此规则的冲突 `static` 。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.StaticMembersFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembersFixed/cs/FxCop.Design.StaticMembersFixed.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1053:静态容器类型不应具有构造函数](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)
