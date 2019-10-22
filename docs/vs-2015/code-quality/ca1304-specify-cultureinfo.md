---
title: CA1304：指定 CultureInfo |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 202f3759026bbedd5e99e94bba76e956b83357b3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661461"
---
# <a name="ca1304-specify-cultureinfo"></a>CA1304：指定 CultureInfo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SpecifyCultureInfo|
|CheckId|CA1304|
|类别|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法或构造函数调用具有接受 <xref:System.Globalization.CultureInfo?displayProperty=fullName> 参数的重载的成员，并且该方法或构造函数不调用采用 <xref:System.Globalization.CultureInfo> 参数的重载。 此规则将忽略对以下方法的调用：

- <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>

## <a name="rule-description"></a>规则说明
 如果未提供 <xref:System.Globalization.CultureInfo> 或 <xref:System.IFormatProvider?displayProperty=fullName> 对象，则重载成员提供的默认值可能不会在所有区域设置中产生所需的效果。 此外，[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 成员根据你的代码可能不正确的假设，选择默认区域性和格式设置。 若要确保代码按方案的预期运行，应根据以下准则提供区域性特定的信息：

- 如果将向用户显示值，则使用当前区域性。 请参阅<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>.

- 如果值将由软件存储和访问（即，保存到文件或数据库），请使用固定区域性。 请参阅<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.

- 如果您不知道值的目标，请使数据使用者或提供者指定区域性。

  请注意，<xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 仅用于通过使用 <xref:System.Resources.ResourceManager?displayProperty=fullName> 类的实例检索已本地化的资源。

  即使重载成员的默认行为适合您的需要，更好的做法是显式调用特定于区域性的重载，以便您的代码是自我记录的，更易于维护。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用采用 <xref:System.Globalization.CultureInfo> 或 <xref:System.IFormatProvider> 的重载，并根据前面列出的准则指定参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果确信默认区域性/格式提供程序是正确的选择，并且代码可维护性不是重要的开发优先级，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在下面的示例中，`BadMethod` 会导致此规则发生两次冲突。 `GoodMethod` 通过将固定区域性传递给 System.string 来更正第一个冲突，并通过将当前区域性传递到 <xref:System.String.ToLower%2A> 来更正第二个冲突，因为 `string3` 向用户显示。

 [!code-csharp[FxCop.Globalization.CultureInfo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.CultureInfo/cs/FxCop.Globalization.CultureInfo.cs#1)]

## <a name="example"></a>示例
 下面的示例演示了当前区域性对 <xref:System.DateTime> 类型所选择的默认 <xref:System.IFormatProvider> 的影响。

 [!code-csharp[FxCop.Globalization.IFormatProvider#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.IFormatProvider/cs/FxCop.Globalization.IFormatProvider.cs#1)]

 本示例生成以下输出。

 **6/4/1900 12:15:12 PM** 
**06/04/1900 12:15:12**
## <a name="related-rules"></a>相关规则
 [CA1305：指定 IFormatProvider](../code-quality/ca1305-specify-iformatprovider.md)

## <a name="see-also"></a>请参阅
 [钢笔尖：使用 CultureInfo 类](https://msdn.microsoft.com/d4329e34-64c3-4d1e-8c73-5b0ee626ba7a)
