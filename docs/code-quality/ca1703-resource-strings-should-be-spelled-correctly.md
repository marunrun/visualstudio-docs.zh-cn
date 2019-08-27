---
title: CA1703:资源字符串应正确拼写
ms.date: 03/28/2018
ms.topic: reference
f1_keywords:
- ResourceStringsShouldBeSpelledCorrectly
- CA1703
helpviewer_keywords:
- CA1703
- ResourceStringsShouldBeSpelledCorrectly
ms.assetid: 693f4970-f512-40cb-ae3b-a0f3a5c6d6f1
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2643ff7cb8ce401462be7e5c1e52d5f985896f3a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546266"
---
# <a name="ca1703-resource-strings-should-be-spelled-correctly"></a>CA1703:资源字符串应正确拼写

|||
|-|-|
|TypeName|ResourceStringsShouldBeSpelledCorrectly|
|CheckId|CA1703|
|类别|Microsoft.Naming|
|是否重大更改|非换行|

## <a name="cause"></a>原因

资源字符串包含一个或多个未被 Microsoft 拼写检查器库识别的单词。

## <a name="rule-description"></a>规则说明

此规则将资源字符串分析为单词 （切分组合词），并检查每个单词/标记的拼写。 有关分析算法的信息，请参阅[CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请使用完整的单词的拼写正确，或向自定义词典添加单词。 有关如何使用自定义词典的信息，请参阅[CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

## <a name="change-the-dictionary-language"></a>更改字典语言

默认情况下，使用拼写检查器的英语 (en) 版本。 如果你想要更改拼写检查器的语言，您可以这样做通过添加下列任一属性到您*AssemblyInfo.cs*或*AssemblyInfo.vb*文件：

- 使用<xref:System.Reflection.AssemblyCultureAttribute>来指定的区域性，如果你的资源位于附属程序集。
- 使用<xref:System.Resources.NeutralResourcesLanguageAttribute>来指定*非特定区域性*的程序集，如果你的资源位于你的代码相同的程序集中。

> [!IMPORTANT]
> 如果将区域性设置为基于英语的区域性之外的任何内容，则以无提示方式禁用此代码分析规则。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 正确的拼写的单词可以减少学习新的软件库所需的时间。

## <a name="related-rules"></a>相关的规则

- [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)
- [CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)
- [CA2204:应正确拼写文本](../code-quality/ca2204-literals-should-be-spelled-correctly.md)