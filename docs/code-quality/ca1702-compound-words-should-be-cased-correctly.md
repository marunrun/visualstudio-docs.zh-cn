---
title: CA1702:组合词应采用正确的大小写
ms.date: 03/28/2018
ms.topic: reference
f1_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
helpviewer_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
ms.assetid: 05481245-7ad8-48c3-a456-3aa44b6160a6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f78ea4f44c48d2740df58def03a6335bce6637a2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545927"
---
# <a name="ca1702-compound-words-should-be-cased-correctly"></a>CA1702:组合词应采用正确的大小写

|||
|-|-|
|TypeName|CompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1702|
|类别|Microsoft.Naming|
|是否重大更改|对程序集引发重大时。<br /><br /> 无间断-如果在类型参数上引发。|

## <a name="cause"></a>原因

标识符的名称包含多个单词，其中至少有一个单词似乎是大小写不正确的组合词。

## <a name="rule-description"></a>规则说明

标识符名称拆分为根据大小写的单词。 通过 Microsoft 拼写检查器库会检查每个连续的两个单词组合。 如果它被识别，该标识符将生成与规则的冲突。 复合词而导致违反了示例包括"CheckSum"和"多部分"应采用的大小写为"Checksum"和"多部分"，分别。 由于以前经常使用，几个例外情况内置规则，并标记了几个单个单词，例如"工具栏"和"Filename"，，应采用的大小写为两个不同的单词 （在此情况下，"工具栏"和"FileName"）。

命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。

## <a name="how-to-fix-violations"></a>如何解决冲突

更改名称，使其具有正确的大小写。

## <a name="language"></a>语言

当前仅对基于英语的区域性字典检查，拼写检查器。 可以通过添加更改项目文件中的项目的区域性**CodeAnalysisCulture**元素。

例如：

```xml
<Project ...>
  <PropertyGroup>
    <CodeAnalysisCulture>en-AU</CodeAnalysisCulture>
```

> [!IMPORTANT]
> 如果将区域性设置为基于英语的区域性之外的任何内容，则以无提示方式禁用此代码分析规则。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，如果由拼写字典中，识别的组合词的两个部分，目的是使用两个单词。

## <a name="related-rules"></a>相关的规则

- [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)
- [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>请参阅

- [命名规则](/dotnet/standard/design-guidelines/naming-guidelines)
- [大小写约定](/dotnet/standard/design-guidelines/capitalization-conventions)