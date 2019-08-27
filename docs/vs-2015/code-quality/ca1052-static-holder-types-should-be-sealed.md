---
title: CA1052:应密封静态容器类型 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d973d7ff5464b76228e917c83b3e62116e115718
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65693806"
---
# <a name="ca1052-static-holder-types-should-be-sealed"></a>CA1052:应密封静态容器类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|StaticHolderTypesShouldBeSealed|
|CheckId|CA1052|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型仅包含静态成员和不使用声明[密封](https://msdn.microsoft.com/library/8e4ed5d3-10be-47db-9488-0da2008e6f3f)([NotInheritable](https://msdn.microsoft.com/library/5c4da7c9-9562-4653-a947-1972e992f9f9)) 修饰符。

## <a name="rule-description"></a>规则说明
 此规则假定只包含静态成员的类型未设计为继承，因为该类型不提供可以在派生类型中重写任何功能。 未计划继承的类型应该用 `sealed` 修饰符进行标记，以便禁止其作为基类型使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，将类型标记为`sealed`。 如果你正面向[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]2.0 或更早版本，更好的方法是将类型标记为`static`。 以这种方式，您无需专用的构造函数，以防止此类创建声明。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当类型能被继承，禁止显示此规则的警告。 如果没有`sealed`修饰符，则表明该类型用作基类型。

## <a name="example-of-a-violation"></a>冲突的示例

### <a name="description"></a>描述
 下面的示例显示了违反了此规则的类型。

### <a name="code"></a>代码
 [!code-cpp[FxCop.Design.StaticMembers#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembers/cpp/FxCop.Design.StaticMembers.cpp#1)]
 [!code-csharp[FxCop.Design.StaticMembers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembers/cs/FxCop.Design.StaticMembers.cs#1)]
 [!code-vb[FxCop.Design.StaticMembers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembers/vb/FxCop.Design.StaticMembers.vb#1)]

## <a name="fix-with-the-static-modifier"></a>使用静态修饰符修复

### <a name="description"></a>描述
 下面的示例演示如何修复该规则的冲突错误的标记与类型`static`修饰符。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.StaticMembersFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticMembersFixed/cs/FxCop.Design.StaticMembersFixed.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1053:静态容器类型不应具有构造函数](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)
