---
title: CA1302：不对区域设置特定的字符串进行硬编码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
helpviewer_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
ms.assetid: 05ed134a-837d-43d7-bf97-906edeac44ce
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6e16fff154b5c0df660b06e5bf9e9e838762adff
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661479"
---
# <a name="ca1302-do-not-hardcode-locale-specific-strings"></a>CA1302：请不要对区域设置特定的字符串进行硬编码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotHardcodeLocaleSpecificStrings|
|CheckId|CA1302|
|类别|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法使用表示某些系统文件夹的部分路径的字符串。

## <a name="rule-description"></a>规则说明
 @No__t_0 枚举包含引用特殊系统文件夹的成员。 这些文件夹的位置在不同的操作系统上可能具有不同的值，用户可以更改某些位置，并且这些位置已本地化。 特殊文件夹的一个示例是系统文件夹，这是 [!INCLUDE[winxp](../includes/winxp-md.md)] 上的 "C:\WINDOWS\system32"，但 [!INCLUDE[win2kfamily](../includes/win2kfamily-md.md)] 上的 "C:\WINNT\system32"。 @No__t_0 方法返回与 <xref:System.Environment.SpecialFolder> 枚举关联的位置。 @No__t_0 返回的位置已本地化，适用于当前正在运行的计算机。

 此规则将使用 <xref:System.Environment.GetFolderPath%2A> 方法检索的文件夹路径切分到不同的目录级别。 每个字符串都与标记进行比较。 如果找到匹配项，则假定方法正在生成一个字符串，该字符串引用与该标记关联的系统位置。 为了实现可移植性和可本地化性，请使用 <xref:System.Environment.GetFolderPath%2A> 方法检索特殊系统文件夹的位置，而不是使用字符串文本。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用 <xref:System.Environment.GetFolderPath%2A> 方法检索位置。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果字符串文本未用于引用与 <xref:System.Environment.SpecialFolder> 枚举关联的系统位置之一，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例生成常见应用程序数据文件夹的路径，该文件夹从此规则生成三个警告。 接下来，该示例使用 <xref:System.Environment.GetFolderPath%2A> 方法检索路径。

 [!code-csharp[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/cs/FxCop.Globalization.HardcodedLocaleStrings.cs#1)]
 [!code-vb[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/vb/FxCop.Globalization.HardcodedLocaleStrings.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1303：不要将文本作为本地化参数传递](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)
