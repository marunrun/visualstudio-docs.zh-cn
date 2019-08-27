---
title: CA1303:不传递文本作为本地化的参数 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: fafcf113f5f40da3bcc4666778330865dcdfb84c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686805"
---
# <a name="ca1303-do-not-pass-literals-as-localized-parameters"></a>CA1303:请不要将文本作为本地化参数传递
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|类别|Microsoft.Globalization|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 一种方法将字符串作为参数传递给构造函数或方法中的[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]类库和字符串应该是可本地化。

 文本字符串作为值传递给参数或属性和一个或多个以下情况下为 true 时，会引发此警告：

- <xref:System.ComponentModel.LocalizableAttribute>参数或属性的特性设置为 true。

- 参数或属性名称包含"Text"、"Message"描述"。

- 传递给 Console.Write 或 Console.WriteLine 方法将字符串参数名称是"值"format"。

## <a name="rule-description"></a>规则说明
 在源代码中嵌入的字符串文本是难以进行本地化。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，将通过的实例检索一个字符串替换为字符串文字<xref:System.Resources.ResourceManager>类。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果没有将本地化代码库，或如果字符串不会公开给最终用户或开发人员使用代码库。

 用户可以消除针对不应传递本地化的字符串通过任一重命名的参数或属性名为，或通过将标记为 conditional 这些项的方法。

## <a name="example"></a>示例
 下面的示例显示了当其两个参数之一不在范围内时，将引发异常的方法。 对于第一个参数，异常构造函数传递与此规则冲突的文字字符串。 对于第二个参数，构造函数正确传递通过检索字符串<xref:System.Resources.ResourceManager>。

 [!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cpp/FxCop.Globalization.DoNotPassLiterals.cpp#1)]
 [!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cs/FxCop.Globalization.DoNotPassLiterals.cs#1)]
 [!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/vb/FxCop.Globalization.DoNotPassLiterals.vb#1)]

## <a name="see-also"></a>请参阅
 [桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
