---
title: CA2112：受保护的类型不应公开字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2112
- SecuredTypesShouldNotExposeFields
helpviewer_keywords:
- SecuredTypesShouldNotExposeFields
- CA2112
ms.assetid: 9eb13a78-3487-49f2-81d1-3c3866db132f
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b9c91a7c9833d3d9d5ae283c28ae4d437bd07734
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658747"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112：受保护的类型不应公开字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型包含公共字段，并受[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)保护。

## <a name="rule-description"></a>规则说明
 如果代码可以访问受链接要求保护的类型的实例，则该代码不必满足此链接要求就可以访问该类型的字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将字段设置为非公共字段，并添加返回字段数据的公共属性或方法。 对类型的 LinkDemand 安全检查保护对类型属性和方法的访问。 但是，代码访问安全性不适用于字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 出于安全问题和良好的设计，你应该通过使公共字段成为非公共字段来解决冲突。 如果字段不包含应保持安全的信息，并且您不依赖于字段的内容，则可以禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例由一个包含不安全字段的库类型（`SecuredTypeWithFields`）、一种类型（`Distributor`），该类型（可创建库类型的实例，并将实例与类型一起传递给类型时不具有创建权限的方法）和应用程序代码（可读取实例的字段，即使它不具有用于保护类型的权限。

 以下库代码违反了该规则。

 [!code-csharp[FxCop.Security.LinkDemandOnField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LinkDemandOnField/cs/FxCop.Security.LinkDemandOnField.cs#1)]

## <a name="example"></a>示例
 应用程序无法创建实例，原因是保护受保护类型的链接要求。 通过以下类，应用程序可以获取受保护类型的实例。

 [!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LDOnFieldsDistributor/cs/FxCop.Security.LDOnFieldsDistributor.cs#1)]

## <a name="example"></a>示例
 下面的应用程序演示了如何在没有权限的情况下访问受保护类型的方法，代码可以访问该类型的字段。

 [!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestLinkDemandOnFields/cs/FxCop.Security.TestLinkDemandOnFields.cs#1)]

 本示例生成以下输出。

 **创建 SecuredTypeWithFields 的实例。** 
**安全类型字段：22、33** 
**更改安全类型的字段 ...** 
**缓存的对象字段：99、33**
## <a name="related-rules"></a>相关规则
 [CA1051：不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>请参阅
 [链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
