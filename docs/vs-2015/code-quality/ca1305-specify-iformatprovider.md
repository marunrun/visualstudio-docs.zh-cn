---
title: CA1305：指定 IFormatProvider |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyIFormatProvider
- CA1305
helpviewer_keywords:
- CA1305
- SpecifyIFormatProvider
ms.assetid: fb34ed9a-4eab-47cc-8eef-3068a4a1397e
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 025d76f8e946dd3021141d6736c6b4bd40d57170
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85539081"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305:指定 IFormatProvider
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|SpecifyIFormatProvider|
|CheckId|CA1305|
|类别|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法或构造函数调用一个或多个具有接受参数的重载的成员 <xref:System.IFormatProvider?displayProperty=fullName> ，并且方法或构造函数不调用采用参数的重载 <xref:System.IFormatProvider> 。 此规则 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 将忽略被记录为忽略 <xref:System.IFormatProvider> 参数和以下方法的方法调用：

- <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>

## <a name="rule-description"></a>规则描述
 如果 <xref:System.Globalization.CultureInfo?displayProperty=fullName> <xref:System.IFormatProvider> 未提供或对象，则重载成员提供的默认值可能不会在所有区域设置中产生所需的效果。 另外，成员还可以根据 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 你的代码可能不正确的假设来选择默认区域性和格式设置。 若要确保代码按方案的预期运行，应根据以下准则提供区域性特定的信息：

- 如果将向用户显示值，则使用当前区域性。 请参阅 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>。

- 如果此值将由软件 (保存并访问) 保存到文件或数据库，请使用固定区域性。 请参阅 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>。

- 如果您不知道值的目标，请使数据使用者或提供者指定区域性。

  请注意， <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 仅用于通过使用类的实例检索已本地化的资源 <xref:System.Resources.ResourceManager?displayProperty=fullName> 。

  即使重载成员的默认行为适合您的需要，更好的做法是显式调用特定于区域性的重载，以便您的代码是自我记录的，更易于维护。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用采用或的重载， <xref:System.Globalization.CultureInfo> <xref:System.IFormatProvider> 并根据前面列出的准则指定参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果确信默认区域性/格式提供程序是正确的选择并且代码可维护性不是重要的开发优先级，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在下面的示例中，将 `BadMethod` 导致此规则发生两次冲突。 `GoodMethod` 通过将固定区域性传递到来更正第一个冲突 <xref:System.String.Compare%2A> ，并通过将当前区域性传递到来更正第二个冲突， <xref:System.String.ToLower%2A> 因为 `string3` 向用户显示。

 [!code-csharp[FxCop.Globalization.CultureInfo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.CultureInfo/cs/FxCop.Globalization.CultureInfo.cs#1)]

## <a name="example"></a>示例
 下面的示例演示当前区域性对由类型选择的默认值的影响 <xref:System.IFormatProvider> <xref:System.DateTime> 。

 [!code-csharp[FxCop.Globalization.IFormatProvider#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.IFormatProvider/cs/FxCop.Globalization.IFormatProvider.cs#1)]

 本示例生成以下输出。

 **6/4/1900 12:15:12 PM** 
**06/04/1900 12:15:12**
## <a name="related-rules"></a>相关规则
 [CA1304:指定 CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>另请参阅
 [钢笔尖：使用 CultureInfo 类](https://msdn.microsoft.com/d4329e34-64c3-4d1e-8c73-5b0ee626ba7a)
