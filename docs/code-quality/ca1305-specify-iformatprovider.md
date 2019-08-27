---
title: CA1305:指定 IFormatProvider
ms.date: 06/30/2018
ms.topic: reference
f1_keywords:
- SpecifyIFormatProvider
- CA1305
helpviewer_keywords:
- CA1305
- SpecifyIFormatProvider
ms.assetid: fb34ed9a-4eab-47cc-8eef-3068a4a1397e
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: eda86085a5a2b8ba8e42116005890d2bda0b1dca
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714685"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305:指定 IFormatProvider

|||
|-|-|
|TypeName|SpecifyIFormatProvider|
|CheckId|CA1305|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因

某方法或构造函数调用的重载接受一个或多个成员<xref:System.IFormatProvider?displayProperty=fullName>参数，该方法或构造函数不调用的重载的<xref:System.IFormatProvider>参数。

此规则将忽略对被记录为忽略的.NET 方法的调用<xref:System.IFormatProvider>参数。 该规则还会忽略以下方法：

- <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>

## <a name="rule-description"></a>规则说明

当<xref:System.Globalization.CultureInfo?displayProperty=nameWithType>或<xref:System.IFormatProvider>未提供对象，则重载成员提供的默认值可能不想要在所有区域设置中起作用。 此外，.NET 成员选择默认区域性，并设置格式基于可能不为你的代码正确的假设。 若要确保代码按预期为方案运行，应提供特定于区域性的信息，按照以下原则：

- 如果将向用户显示的值，则使用当前区域性。 请参阅 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>。

- 如果的值将存储并访问的软件 （保存到文件或数据库），使用固定区域性。 请参阅 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>。

- 如果不知道的值的目标，具有数据使用者或提供程序指定的区域性。

即使重载的成员的默认行为是适用于你的需求，则最好显式调用特定于区域性的重载，因此，你的代码是一目了然，且更易维护。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请使用采用重载<xref:System.IFormatProvider>参数。 或者，使用[C# 内插字符串](/dotnet/csharp/tutorials/string-interpolation)并将其传递给<xref:System.FormattableString.Invariant%2A?displayProperty=nameWithType>方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告时确定的默认格式是正确的选择，并且代码可维护性不是一个重要开发的优先级。

## <a name="example"></a>示例

在下面的代码，`example1`字符串违反规则 CA1305。 `example2`字符串将传递满足规则 CA1305 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>，它可以实现<xref:System.IFormatProvider>到<xref:System.String.Format(System.IFormatProvider,System.String,System.Object)?displayProperty=nameWithType>。 `example3`字符串内插的字符串到表示通过满足规则 CA1305 <xref:System.FormattableString.Invariant%2A?displayProperty=fullName]>。

```csharp
string name = "Georgette";

// Violates CA1305
string example1 = String.Format("Hello {0}", name);

// Satisfies CA1305
string example2 = String.Format(CultureInfo.CurrentCulture, "Hello {0}", name);

// Satisfies CA1305
string example3 = FormattableString.Invariant($"Hello {name}");
```

## <a name="related-rules"></a>相关的规则

- [CA1304:指定 CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>请参阅

- [使用 CultureInfo 类](/dotnet/standard/globalization-localization/globalization#work-with-culture-specific-settings)