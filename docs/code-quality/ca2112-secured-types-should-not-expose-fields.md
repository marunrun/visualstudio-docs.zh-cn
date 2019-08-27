---
title: CA2112:受保护的类型不应公开字段
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2112
- SecuredTypesShouldNotExposeFields
helpviewer_keywords:
- SecuredTypesShouldNotExposeFields
- CA2112
ms.assetid: 9eb13a78-3487-49f2-81d1-3c3866db132f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 43ef4165823f59045dda8c05b5679fdd3b795114
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921081"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112:受保护的类型不应公开字段

|||
|-|-|
|TypeName|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
公共或受保护类型包含公共字段, 并受[链接要求](/dotnet/framework/misc/link-demands)保护。

## <a name="rule-description"></a>规则说明
如果代码可以访问受链接要求保护的类型的实例，则该代码不必满足此链接要求就可以访问该类型的字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将字段设置为非公共字段, 并添加返回字段数据的公共属性或方法。 对类型的 LinkDemand 安全检查保护对类型属性和方法的访问。 但是, 代码访问安全性不适用于字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
出于安全问题和良好的设计, 你应该通过使公共字段成为非公共字段来解决冲突。 如果字段不包含应保持安全的信息, 并且您不依赖于字段的内容, 则可以禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例由一个包含不安全字段的`SecuredTypeWithFields`库类型 () 组成, 这种`Distributor`类型 () 可以创建库类型的实例, 并将实例传递给类型时不具有创建它们的权限, 而应用程序代码则即使不具有用于保护类型的权限, 也可以读取实例的字段。

以下库代码违反了该规则。

[!code-csharp[FxCop.Security.LinkDemandOnField#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_1.cs)]

## <a name="example-1"></a>示例 1
应用程序无法创建实例, 原因是保护受保护类型的链接要求。 通过以下类, 应用程序可以获取受保护类型的实例。

[!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_2.cs)]

## <a name="example-2"></a>示例 2
下面的应用程序演示了如何在没有权限的情况下访问受保护类型的方法, 代码可以访问该类型的字段。

[!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_3.cs)]

该示例产生下面的输出：

```txt
Creating an instance of SecuredTypeWithFields.
Secured type fields: 22, 33
Changing secured type's field...
Cached Object fields: 99, 33
```

## <a name="related-rules"></a>相关规则

- [CA1051不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>请参阅

- [链接需求](/dotnet/framework/misc/link-demands)
- [数据和建模](/dotnet/framework/data/index)