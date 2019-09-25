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
ms.openlocfilehash: a9f6c8fd44749de43d86bf8037df0130ad682321
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235036"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305:指定 IFormatProvider

|||
|-|-|
|TypeName|SpecifyIFormatProvider|
|CheckId|CA1305|
|类别|Microsoft.Globalization|
|重大更改|不间断|

## <a name="cause"></a>原因

方法或构造函数调用一个或多个具有接受<xref:System.IFormatProvider?displayProperty=fullName>参数的重载的成员，并且方法或构造函数不调用<xref:System.IFormatProvider>采用参数的重载。

此规则将忽略被记录为忽略<xref:System.IFormatProvider>参数的 .net 方法的调用。 此规则还会忽略以下方法：

- <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>

## <a name="rule-description"></a>规则说明

如果未提供<xref:System.IFormatProvider>或对象，则重载成员提供的默认值可能不会在所有区域设置中产生所需的效果。 <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> 此外，.NET 成员还可以根据你的代码可能不正确的假设来选择默认区域性和格式设置。 若要确保代码按方案的预期运行，应根据以下准则提供区域性特定的信息：

- 如果将向用户显示值，则使用当前区域性。 请参阅 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>。

- 如果值将由软件存储和访问（保存到文件或数据库），请使用固定区域性。 请参阅 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>。

- 如果您不知道值的目标，请使数据使用者或提供者指定区域性。

即使重载成员的默认行为适合您的需要，更好的做法是显式调用特定于区域性的重载，以便您的代码是自我记录的，更易于维护。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请使用采用<xref:System.IFormatProvider>自变量的重载。 或者，使用内[ C#插字符串](/dotnet/csharp/tutorials/string-interpolation)并将<xref:System.FormattableString.Invariant%2A?displayProperty=nameWithType>其传递给方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果确信默认格式是正确的选择，则可以安全地禁止显示此规则发出的警告，而代码可维护性并不是一个重要的开发优先级。

## <a name="example"></a>示例

在下面的代码中， `example1`字符串违反规则 CA1305。 字符串满足规则 CA1305，方法是<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>将实现<xref:System.IFormatProvider>的传递到<xref:System.String.Format(System.IFormatProvider,System.String,System.Object)?displayProperty=nameWithType>。 `example2` 通过将内插字符串传递到<xref:System.FormattableString.Invariant%2A?displayProperty=fullName]>，字符串满足规则CA1305。`example3`

```csharp
string name = "Georgette";

// Violates CA1305
string example1 = String.Format("Hello {0}", name);

// Satisfies CA1305
string example2 = String.Format(CultureInfo.CurrentCulture, "Hello {0}", name);

// Satisfies CA1305
string example3 = FormattableString.Invariant($"Hello {name}");
```

## <a name="related-rules"></a>相关规则

- [CA1304指定 CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>请参阅

- [使用 CultureInfo 类](/dotnet/standard/globalization-localization/globalization#work-with-culture-specific-settings)