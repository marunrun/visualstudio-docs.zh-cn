---
title: CA2119:密封满足私有接口的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SealMethodsThatSatisfyPrivateInterfaces
- CA2119
helpviewer_keywords:
- CA2119
- SealMethodsThatSatisfyPrivateInterfaces
ms.assetid: 483d02e1-cfaf-4754-a98f-4116df0f3509
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 56b08d1b842e65e1c1c29a7409813c314cbf014d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687274"
---
# <a name="ca2119-seal-methods-that-satisfy-private-interfaces"></a>CA2119:密封满足私有接口的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SealMethodsThatSatisfyPrivateInterfaces|
|CheckId|CA2119|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 可继承的公共类型提供的可重写的方法实现`internal`(`Friend`在 Visual Basic 中) 接口。

## <a name="rule-description"></a>规则说明
 接口方法具有公共可访问性，实现的类型不能更改。 内部接口创建一个不应定义的接口的程序集外部实现的协定。 实现内部接口使用的方法的公共类型`virtual`(`Overridable`在 Visual Basic 中) 修饰符允许由程序集外部的派生类型中被重写的方法。 如果中定义的程序集中的第二个类型调用方法，并需要仅限内部使用的协定，而是执行重写的方法中的外部程序集时，可能泄露行为。 这会产生安全漏洞。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，防止方法被重写程序集外部的通过使用以下项之一：

- 请声明类型`sealed`(`NotInheritable`在 Visual Basic 中)。

- 更改到的声明类型的可访问性`internal`(`Friend`在 Visual Basic 中)。

- 从声明类型中删除所有公共构造函数。

- 实现方法，而无需使用`virtual`修饰符。

- 显式实现该方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 则可以安全地禁止显示此警告规则，仔细检查后没有安全存在问题的情况，可能是在程序集外重写该方法的情况下可利用。

## <a name="example"></a>示例
 下面的示例演示一种类型， `BaseImplementation`，这违反了此规则。

 [!code-cpp[FxCop.Security.SealMethods1#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cpp/FxCop.Security.SealMethods1.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cs/FxCop.Security.SealMethods1.cs#1)]
 [!code-vb[FxCop.Security.SealMethods1#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/vb/FxCop.Security.SealMethods1.vb#1)]

## <a name="example"></a>示例
 下面的示例利用前面的示例的虚拟方法实现。

 [!code-cpp[FxCop.Security.SealMethods2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cpp/FxCop.Security.SealMethods2.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cs/FxCop.Security.SealMethods2.cs#1)]
 [!code-vb[FxCop.Security.SealMethods2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/vb/FxCop.Security.SealMethods2.vb#1)]

## <a name="see-also"></a>请参阅
 [接口](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)[接口](https://msdn.microsoft.com/library/61b06674-12c9-430b-be68-cc67ecee1f5b)
