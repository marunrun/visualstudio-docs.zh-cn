---
title: CA1304:指定 CultureInfo
ms.date: 06/30/2018
ms.topic: reference
f1_keywords:
- SpecifyCultureInfo
- CA1304
helpviewer_keywords:
- SpecifyCultureInfo
- CA1304
ms.assetid: b912d76a-54fd-4c93-b25d-16491e0ae319
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f6d4776f6bcbf89e95301bd2c7ef4f6f6b5680d9
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714356"
---
# <a name="ca1304-specify-cultureinfo"></a>CA1304:指定 CultureInfo

|||
|-|-|
|TypeName|SpecifyCultureInfo|
|CheckId|CA1304|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因

方法或构造函数调用的成员具有重载接受<xref:System.Globalization.CultureInfo?displayProperty=nameWithType>参数，该方法或构造函数不调用的重载的<xref:System.Globalization.CultureInfo>参数。 此规则将忽略对以下方法的调用：

- <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>

## <a name="rule-description"></a>规则说明

当<xref:System.Globalization.CultureInfo>或<xref:System.IFormatProvider?displayProperty=nameWithType>未提供对象，则重载成员提供的默认值可能不想要在所有区域设置中起作用。 此外，.NET 成员选择默认区域性，并设置格式基于可能不为你的代码正确的假设。 若要确保代码按预期运行您的环境，应提供特定于区域性的信息，根据以下指导原则：

- 如果将向用户显示的值，则使用当前区域性。 请参阅 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>。

- 如果的值将存储并访问软件，即持久保存到文件或数据库，使用固定区域性。 请参阅 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>。

- 如果不知道的值的目标，具有数据使用者或提供程序指定的区域性。

即使重载的成员的默认行为是适用于你的需求，则最好显式调用特定于区域性的重载，因此，你的代码是一目了然，且更易维护。

> [!NOTE]
> <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 仅用于使用的实例中检索本地化的资源<xref:System.Resources.ResourceManager?displayProperty=nameWithType>类。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请使用采用重载<xref:System.Globalization.CultureInfo>参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告时确定的默认区域性是正确的选择，并且代码可维护性不是一个重要开发的优先级。

## <a name="example-showing-how-to-fix-violations"></a>演示如何修复冲突示例

在以下示例中，`BadMethod`会导致两个违反此规则。 `GoodMethod` 更正通过将传递到固定区域性的第一个冲突<xref:System.String.Compare%2A?displayProperty=nameWithType>，并通过将传递到的当前区域性更正第二个冲突<xref:System.String.ToLower%2A?displayProperty=nameWithType>因为`string3`向用户显示。

[!code-csharp[FxCop.Globalization.CultureInfo#1](../code-quality/codesnippet/CSharp/ca1304-specify-cultureinfo_1.cs)]

## <a name="example-showing-formatted-output"></a>示例显示格式的输出

下面的示例演示在默认的当前区域性的影响<xref:System.IFormatProvider>情况下选择<xref:System.DateTime>类型。

[!code-csharp[FxCop.Globalization.IFormatProvider#1](../code-quality/codesnippet/CSharp/ca1304-specify-cultureinfo_2.cs)]

该示例产生下面的输出：

```txt
6/4/1900 12:15:12 PM
06/04/1900 12:15:12
```

## <a name="related-rules"></a>相关的规则

- [CA1305:指定 IFormatProvider](../code-quality/ca1305-specify-iformatprovider.md)

## <a name="see-also"></a>请参阅

- [使用 CultureInfo 类](/dotnet/standard/globalization-localization/globalization#work-with-culture-specific-settings)