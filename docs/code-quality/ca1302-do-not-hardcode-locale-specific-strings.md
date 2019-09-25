---
title: CA1302:请不要对区域设置特定的字符串进行硬编码
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
helpviewer_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
ms.assetid: 05ed134a-837d-43d7-bf97-906edeac44ce
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 69b6256f2c6ae54467eb21cc17d50119b3c67a9f
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235181"
---
# <a name="ca1302-do-not-hardcode-locale-specific-strings"></a>CA1302:请不要对区域设置特定的字符串进行硬编码

|||
|-|-|
|TypeName|DoNotHardcodeLocaleSpecificStrings|
|CheckId|CA1302|
|类别|Microsoft.Globalization|
|重大更改|不间断|

## <a name="cause"></a>原因
方法使用表示某些系统文件夹的部分路径的字符串。

## <a name="rule-description"></a>规则说明
<xref:System.Environment.SpecialFolder?displayProperty=fullName>枚举包含引用特殊系统文件夹的成员。 这些文件夹的位置在不同的操作系统上可能具有不同的值，用户可以更改某些位置，并且这些位置已本地化。 例如，"C:\WINDOWS\system32" 是中[!INCLUDE[winxp](../code-quality/includes/winxp_md.md)]的 "C:\WINNT\system32 [!INCLUDE[win2kfamily](../code-quality/includes/win2kfamily_md.md)]"，这是一个特殊文件夹的示例。 <xref:System.Environment.GetFolderPath%2A?displayProperty=fullName>方法返回<xref:System.Environment.SpecialFolder>与枚举关联的位置。 返回的位置<xref:System.Environment.GetFolderPath%2A>已本地化，适用于当前正在运行的计算机。

此规则切分使用<xref:System.Environment.GetFolderPath%2A>方法将检索的文件夹路径分成不同的目录级别。 每个字符串都与标记进行比较。 如果找到匹配项，则假定方法正在生成一个字符串，该字符串引用与该标记关联的系统位置。 为了实现可移植性和可<xref:System.Environment.GetFolderPath%2A>本地化性，请使用方法检索特殊系统文件夹的位置，而不是使用字符串文本。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请使用<xref:System.Environment.GetFolderPath%2A>方法检索位置。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果字符串文本未用于引用与<xref:System.Environment.SpecialFolder>枚举关联的系统位置之一，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例生成常见应用程序数据文件夹的路径，该文件夹从此规则生成三个警告。 接下来，该示例使用<xref:System.Environment.GetFolderPath%2A>方法检索路径。

[!code-csharp[FxCop.Globalization.HardcodedLocaleStrings#1](../code-quality/codesnippet/CSharp/ca1302-do-not-hardcode-locale-specific-strings_1.cs)]
[!code-vb[FxCop.Globalization.HardcodedLocaleStrings#1](../code-quality/codesnippet/VisualBasic/ca1302-do-not-hardcode-locale-specific-strings_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1303不要将文本作为本地化参数传递](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)