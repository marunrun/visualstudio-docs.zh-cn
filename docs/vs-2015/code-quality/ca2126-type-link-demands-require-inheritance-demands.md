---
title: CA2126:类型链接请求需要继承请求 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2126
- TypeLinkDemandsRequireInheritanceDemands
helpviewer_keywords:
- CA2126
- TypeLinkDemandsRequireInheritanceDemands
ms.assetid: 07b604e5-5579-4df9-a578-dadd0d8370a7
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8aee10059e9c50e7f572c6fb784da7b97f323905
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687235"
---
# <a name="ca2126-type-link-demands-require-inheritance-demands"></a>CA2126:类型链接请求需要继承请求
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TypeLinkDemandsRequireInheritanceDemands|
|CheckId|CA2126|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 一个公共的非密封的类型受保护的链接要求，具有可重写的方法，并且类型和方法都不受继承要求保护。

## <a name="rule-description"></a>规则说明
 对方法或其声明类型链接请求要求直接调用方的方法具有指定的权限。 在方法上的继承请求要求重写方法，以使指定的权限。 对一种类型的继承请求要求派生类具有指定的权限。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，安全的类型或方法替换为链接要求相同的权限继承要求。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。

 [!code-cpp[FxCop.Security.TypesWithLinkDemands#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/cpp/FxCop.Security.TypesWithLinkDemands.cpp#1)]
 [!code-csharp[FxCop.Security.TypesWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/cs/FxCop.Security.TypesWithLinkDemands.cs#1)]
 [!code-vb[FxCop.Security.TypesWithLinkDemands#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/vb/FxCop.Security.TypesWithLinkDemands.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2108:检查有关值类型的声明性安全](../code-quality/ca2108-review-declarative-security-on-value-types.md)

 [CA2112:受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA2122:不要间接公开方法使用链接请求](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)

 [CA2123:重写链接请求应与基相同](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)

## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[继承需求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[需求](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)
