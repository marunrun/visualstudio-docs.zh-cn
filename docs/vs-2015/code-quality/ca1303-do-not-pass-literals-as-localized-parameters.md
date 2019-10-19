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
ms.openlocfilehash: ce85a3a933d9453c63ef118d5dfd9e0b17cbf130
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661446"
---
# <a name="ca1303-do-not-pass-literals-as-localized-parameters"></a>CA1303：不要将文本作为本地化参数传递
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|类别|Microsoft 全球化|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 方法将字符串文本作为参数传递给 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类库中的构造函数或方法，并且该字符串应可本地化。

 当文字字符串作为值传递到参数或属性，并且满足以下一个或多个条件时，将引发此警告：

- 参数或属性的 <xref:System.ComponentModel.LocalizableAttribute> 特性设置为 true。

- 参数或属性名称包含 "文本"、"消息" 或 "标题"。

- 传递给控制台. Write 或 Console 方法的字符串参数的名称为 "value" 或 "format"。

## <a name="rule-description"></a>规则说明
 嵌入在源代码中的字符串难以本地化。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将字符串文本替换为通过 <xref:System.Resources.ResourceManager> 类的实例检索到的字符串。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果代码库不是本地化的，或者如果不是使用代码库向最终用户公开的开发人员，则可以安全地禁止显示此规则发出的警告。

 用户可以通过重命名参数或名为的属性，或将这些项标记为条件，消除不应传递本地化字符串的方法的干扰。

## <a name="example"></a>示例
 下面的示例演示一个方法，该方法在其两个参数均超出范围时引发异常。 对于第一个参数，将向异常构造函数传递一个与此规则冲突的文本字符串。 对于第二个参数，构造函数会正确传递通过 <xref:System.Resources.ResourceManager> 检索到的字符串。

 [!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cpp/FxCop.Globalization.DoNotPassLiterals.cpp#1)]
 [!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cs/FxCop.Globalization.DoNotPassLiterals.cs#1)]
 [!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/vb/FxCop.Globalization.DoNotPassLiterals.vb#1)]

## <a name="see-also"></a>请参阅
 [桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
