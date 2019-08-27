---
title: CA2112:受保护的类型不应公开字段 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 17a52b952437ce136773d796972c6619a9733749
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687328"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112:受保护的类型不应公开字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型包含公共字段，并受[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)。

## <a name="rule-description"></a>规则说明
 如果代码可以访问受链接要求保护的类型的实例，则该代码不必满足此链接要求就可以访问该类型的字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，字段设为非公共，并添加公共属性或方法返回的字段数据。 LinkDemand 安全检查类型保护对该类型的属性和方法的访问。 但是，代码访问安全性不适用于字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 安全问题并获得良好的设计，您应公共字段非公共，从而解决冲突。 如果字段不会保存信息应保持安全，则可以禁止显示此规则的警告，您不依赖于字段的内容。

## <a name="example"></a>示例
 下面的示例组成的库类型 (`SecuredTypeWithFields`) 包含不安全的字段，一种类型 (`Distributor`)，可以创建库类型的实例和错误的传递到类型的实例没有权限来创建它们，和应用程序代码可以读取实例的字段，即使它没有保护类型的权限。

 以下库代码违反了此规则。

 [!code-csharp[FxCop.Security.LinkDemandOnField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LinkDemandOnField/cs/FxCop.Security.LinkDemandOnField.cs#1)]

## <a name="example"></a>示例
 由于链接要求保护受保护的类型，该应用程序无法创建实例。 下面的类使应用程序以获取受保护的类型的实例。

 [!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LDOnFieldsDistributor/cs/FxCop.Security.LDOnFieldsDistributor.cs#1)]

## <a name="example"></a>示例
 以下应用程序演示了如何，如果没有权限访问受保护的类型的方法，代码可以访问其字段。

 [!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestLinkDemandOnFields/cs/FxCop.Security.TestLinkDemandOnFields.cs#1)]

 本示例生成以下输出。

 **正在创建 SecuredTypeWithFields 的实例。** 
**安全类型的字段：22、 33**
**更改受保护的类型字段...** 
**缓存对象字段：99, 33**
## <a name="related-rules"></a>相关的规则
 [CA1051:不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>请参阅
 [链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
