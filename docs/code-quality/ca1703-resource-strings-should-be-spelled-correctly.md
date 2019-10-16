---
title: CA1703：资源字符串应正确拼写
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
ms.openlocfilehash: c37e07d6259c4229999ff7d4068400c788369e86
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72348957"
---
# <a name="ca1703-resource-strings-should-be-spelled-correctly"></a>CA1703：资源字符串应正确拼写

|||
|-|-|
|TypeName|ResourceStringsShouldBeSpelledCorrectly|
|CheckId|CA1703|
|类别|Microsoft。命名|
|重大更改|不间断|

## <a name="cause"></a>原因

资源字符串包含一个或多个未被 Microsoft 拼写检查器库识别的单词。

## <a name="rule-description"></a>规则说明

此规则将资源字符串分析为单词（词汇切分组合词），并检查每个单词/标记的拼写。 有关分析算法的信息，请参阅[CA1704：标识符应拼写正确](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请使用拼写正确的完整单词，或将单词添加到自定义字典中。 有关如何使用自定义字典的信息，请参阅[CA1704：标识符应拼写正确](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

## <a name="change-the-dictionary-language"></a>更改字典语言

默认情况下，使用英语（en）版本的拼写检查器。 如果要更改拼写检查器的语言，可以通过将以下属性之一添加到*AssemblyInfo.cs*或*AssemblyInfo*文件来执行此操作：

- 如果资源位于附属程序集中，请使用 <xref:System.Reflection.AssemblyCultureAttribute> 来指定区域性。
- 如果资源与代码位于同一程序集中，请使用 <xref:System.Resources.NeutralResourcesLanguageAttribute> 指定程序集的*非特定区域性*。

> [!IMPORTANT]
> 如果将区域性设置为非基于英语的区域性，则此代码分析规则将以静默方式禁用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 拼写正确的单词可减少学习新软件库所需的时间。

## <a name="related-rules"></a>相关规则

- [CA1701：资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)
- [CA1704：标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)
- [CA2204：应正确拼写文本](../code-quality/ca2204.md)