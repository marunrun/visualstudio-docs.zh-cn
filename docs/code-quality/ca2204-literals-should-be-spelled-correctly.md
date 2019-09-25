---
title: CA2204:文字应正确拼写
ms.date: 03/28/2018
ms.topic: reference
f1_keywords:
- Literals should be spelled correctly
- CA2204
- LiteralsShouldBeSpelledCorrectly
helpviewer_keywords:
- CA2204
ms.assetid: b0bbcbb6-c92d-4c14-8ef7-9c8b38c791a6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6763fd9f8999bd590511026f6571db6a747c43bc
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231846"
---
# <a name="ca2204-literals-should-be-spelled-correctly"></a>CA2204:文字应正确拼写

|||
|-|-|
|TypeName|LiteralsShouldBeSpelledCorrectly|
|CheckId|CA2204|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

文本字符串作为可本地化参数的参数或可本地化的属性进行传递，且该字符串包含 Microsoft 拼写检查器库无法识别的一个或多个字词。

## <a name="rule-description"></a>规则说明

如果以下一个或多个条件为 true，则此规则将检查作为值传递到参数或属性的文本字符串：

- 参数或属性的属性设置为true。<xref:System.ComponentModel.LocalizableAttribute>

- 参数或属性名称包含 "文本"、"消息" 或 "标题"。

- 传递给<xref:System.Console.Write%2A>或<xref:System.Console.WriteLine>方法的字符串变量的名称为 "value" 或 "format"。

此规则将文本字符串分析为单词，词汇切分复合词，并检查每个单词或标记的拼写。 有关分析算法的信息，请参阅[CA1704：标识符应拼写正确](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

## <a name="language"></a>语言

拼写检查器当前仅检查基于英语的区域性词典。 通过添加**CodeAnalysisCulture**元素，可以更改项目文件中项目的区域性。

例如:

```xml
<Project ...>
  <PropertyGroup>
    <CodeAnalysisCulture>en-AU</CodeAnalysisCulture>
```

> [!IMPORTANT]
> 如果将区域性设置为非基于英语的区域性，则此代码分析规则将以静默方式禁用。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请更正单词的拼写，或将该词添加到自定义字典中。 有关如何使用自定义字典的信息，请[参阅如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 拼写正确的单词减少了新软件库所需的学习曲线。

## <a name="related-rules"></a>相关规则

- [CA1704标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)
- [CA1703资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)