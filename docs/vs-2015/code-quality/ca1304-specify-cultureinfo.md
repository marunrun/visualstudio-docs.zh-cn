---
title: CA1304:指定 CultureInfo |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyCultureInfo
- CA1304
helpviewer_keywords:
- SpecifyCultureInfo
- CA1304
ms.assetid: b912d76a-54fd-4c93-b25d-16491e0ae319
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f5d4333508d6faec3df81f860f5b5b2b526be324
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692086"
---
# <a name="ca1304-specify-cultureinfo"></a>CA1304:指定 CultureInfo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SpecifyCultureInfo|
|CheckId|CA1304|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 方法或构造函数调用的成员具有重载接受<xref:System.Globalization.CultureInfo?displayProperty=fullName>参数，该方法或构造函数不调用的重载的<xref:System.Globalization.CultureInfo>参数。 此规则将忽略对以下方法的调用：

- <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>

## <a name="rule-description"></a>规则说明
 当<xref:System.Globalization.CultureInfo>或<xref:System.IFormatProvider?displayProperty=fullName>未提供对象，则重载成员提供的默认值可能不想要在所有区域设置中起作用。 此外，[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]成员选择默认区域性和格式设置基于可能不为你的代码正确的假设。 若要确保代码按预期运行您的环境，应提供特定于区域性的信息，根据以下指导原则：

- 如果将向用户显示的值，则使用当前区域性。 请参阅 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>。

- 如果的值将存储并访问软件，即持久保存到文件或数据库，使用固定区域性。 请参阅 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>。

- 如果不知道的值的目标，具有数据使用者或提供程序指定的区域性。

  请注意，<xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>仅用于使用的实例中检索本地化的资源<xref:System.Resources.ResourceManager?displayProperty=fullName>类。

  即使重载的成员的默认行为是适用于你的需求，则最好显式调用特定于区域性的重载，因此，你的代码是一目了然，且更易维护。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请使用接受的重载<xref:System.Globalization.CultureInfo>或<xref:System.IFormatProvider>和指定的参数根据前面已列出的准则。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告时确定的默认区域性/格式提供程序是正确的选择，并且代码可维护性不是一个重要开发的优先级。

## <a name="example"></a>示例
 在以下示例中，`BadMethod`会导致两个违反此规则。 `GoodMethod` 通过将固定区域性传递给 System.String.Compare，更正第一个冲突并通过将传递到的当前区域性更正第二个冲突<xref:System.String.ToLower%2A>因为`string3`向用户显示。

 [!code-csharp[FxCop.Globalization.CultureInfo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.CultureInfo/cs/FxCop.Globalization.CultureInfo.cs#1)]

## <a name="example"></a>示例
 下面的示例演示在默认的当前区域性的影响<xref:System.IFormatProvider>情况下选择<xref:System.DateTime>类型。

 [!code-csharp[FxCop.Globalization.IFormatProvider#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.IFormatProvider/cs/FxCop.Globalization.IFormatProvider.cs#1)]

 本示例生成以下输出。

 **1900 年 6 月 4 日下午 12:15:12**
**06/04/1900年 12:15:12**
## <a name="related-rules"></a>相关的规则
 [CA1305:指定 IFormatProvider](../code-quality/ca1305-specify-iformatprovider.md)

## <a name="see-also"></a>请参阅
 [NIB：使用 CultureInfo 类](https://msdn.microsoft.com/d4329e34-64c3-4d1e-8c73-5b0ee626ba7a)
