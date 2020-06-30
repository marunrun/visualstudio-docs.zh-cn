---
title: CA1303：不要将文本作为本地化参数传递 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Do not pass literals as localized parameters
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
helpviewer_keywords:
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
ms.assetid: 904d284e-76d0-4b8f-a4df-0094de8d7aac
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f3ad1f56215d002c03d346b38ce6155e8df7412b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539108"
---
# <a name="ca1303-do-not-pass-literals-as-localized-parameters"></a>CA1303:请不要将文本作为本地化参数传递
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|Category|Microsoft 全球化|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 方法将字符串文本作为参数传递到类库中的构造函数或方法 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ，并且该字符串应可本地化。

 当文字字符串作为值传递到参数或属性，并且满足以下一个或多个条件时，将引发此警告：

- <xref:System.ComponentModel.LocalizableAttribute>参数或属性的属性设置为 true。

- 参数或属性名称包含 "文本"、"消息" 或 "标题"。

- 传递给控制台. Write 或 Console 方法的字符串参数的名称为 "value" 或 "format"。

## <a name="rule-description"></a>规则描述
 嵌入在源代码中的字符串难以本地化。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将字符串文本替换为通过类的实例检索到的字符串 <xref:System.Resources.ResourceManager> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果代码库不是本地化的，或者如果不是使用代码库向最终用户公开的开发人员，则可以安全地禁止显示此规则发出的警告。

 用户可以通过重命名参数或名为的属性，或将这些项标记为条件，消除不应传递本地化字符串的方法的干扰。

## <a name="example"></a>示例
 下面的示例演示一个方法，该方法在其两个参数均超出范围时引发异常。 对于第一个参数，将向异常构造函数传递一个与此规则冲突的文本字符串。 对于第二个参数，构造函数会正确地传递通过检索的字符串 <xref:System.Resources.ResourceManager> 。

 [!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cpp/FxCop.Globalization.DoNotPassLiterals.cpp#1)]
 [!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cs/FxCop.Globalization.DoNotPassLiterals.cs#1)]
 [!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/vb/FxCop.Globalization.DoNotPassLiterals.vb#1)]

## <a name="see-also"></a>另请参阅
 [桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
