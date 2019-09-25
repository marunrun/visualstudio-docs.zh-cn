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
ms.openlocfilehash: 5480d3dde926dfe31b018a5cd0b1ea6a5813063b
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234338"
---
# <a name="ca1702-compound-words-should-be-cased-correctly"></a>CA1702:组合词应采用正确的大小写

|||
|-|-|
|TypeName|CompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1702|
|类别|Microsoft.Naming|
|重大更改|重大-对程序集引发时。<br /><br /> 不间断-在类型参数上触发时。|

## <a name="cause"></a>原因

标识符的名称包含多个单词，其中至少有一个单词似乎是大小写不正确的组合词。

## <a name="rule-description"></a>规则说明

标识符的名称拆分为基于大小写的单词。 Microsoft 拼写检查器库检查每个连续两个单词的组合。 如果识别，标识符将生成规则冲突。 导致冲突的组合词的示例包括 "CheckSum" 和 "多部分"，分别应以 "Checksum" 和 "多部分" 的大小写形式。 由于以前的常见用法，规则中内置了几个例外，并标记了几个单个字词（如 "Toolbar" 和 "Filename"），其大小写应为两个不同的单词（在本例中为 "ToolBar" 和 "FileName"）。

命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突

更改名称，使其大小写正确。

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

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果拼写字典识别了复合单词的两个部分，则可以安全地禁止显示此规则发出的警告，并使用两个词。

## <a name="related-rules"></a>相关规则

- [CA1701资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)
- [CA1709标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708标识符的差别应超过大小写](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>请参阅

- [命名规则](/dotnet/standard/design-guidelines/naming-guidelines)
- [大小写约定](/dotnet/standard/design-guidelines/capitalization-conventions)