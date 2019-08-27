---
title: CA1701:资源字符串组合词应采用正确的大小写
ms.date: 03/28/2018
ms.topic: reference
f1_keywords:
- ResourceStringCompoundWordsShouldBeCasedCorrectly
- CA1701
helpviewer_keywords:
- CA1701
- ResourceStringCompoundWordsShouldBeCasedCorrectly
ms.assetid: 4ddbe09f-24b8-4c47-9373-a06f4487ca0d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8fdae06137586f11de1a30a73894c46c7fb18fa6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546279"
---
# <a name="ca1701-resource-string-compound-words-should-be-cased-correctly"></a>CA1701:资源字符串组合词应采用正确的大小写

|||
|-|-|
|TypeName|ResourceStringCompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1701|
|类别|Microsoft.Naming|
|是否重大更改|非换行|

## <a name="cause"></a>原因

包含的资源字符串似乎不正确的大小写一个组合词。

## <a name="rule-description"></a>规则说明

每个单词中的资源字符串拆分为根据大小写的令牌。 Microsoft 拼写检查器库会对由两个连续的标记构成的每个组合进行检查。 如果被识别，该单词将生成规则冲突。 复合词而导致违反了示例包括"CheckSum"和"多部分"应采用的大小写为"Checksum"和"多部分"，分别。 由于以前经常使用，几个例外情况内置规则，并将标记了几个单个单词，例如"工具栏"和"文件名"，应为两个不同单词的大小写。 在此示例中，将标记"工具栏"和"FileName"。

命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。

## <a name="how-to-fix-violations"></a>如何解决冲突

更改单词，使其具有正确的大小写。

## <a name="change-the-dictionary-language"></a>更改字典语言

默认情况下，使用拼写检查器的英语 (en) 版本。 如果你想要更改拼写检查器的语言，您可以这样做通过添加下列任一属性到您*AssemblyInfo.cs*或*AssemblyInfo.vb*文件：

- 使用<xref:System.Reflection.AssemblyCultureAttribute>来指定的区域性，如果你的资源位于附属程序集。
- 使用<xref:System.Resources.NeutralResourcesLanguageAttribute>来指定*非特定区域性*的程序集，如果你的资源位于你的代码相同的程序集中。

> [!IMPORTANT]
> 如果将区域性设置为基于英语的区域性之外的任何内容，则以无提示方式禁用此代码分析规则。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，如果这两个部件的组合词识别由拼写字典，目的是使用两个单词。

此外可以为用于拼写检查器的自定义字典添加组合词。 自定义字典中的单词不会导致冲突。 有关详细信息，请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)。

## <a name="related-rules"></a>相关的规则

- [CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)
- [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>请参阅

- [大小写约定](/dotnet/standard/design-guidelines/capitalization-conventions)
- [命名规则](/dotnet/standard/design-guidelines/naming-guidelines)