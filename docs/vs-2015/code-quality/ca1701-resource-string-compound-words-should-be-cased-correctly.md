---
title: CA1701:资源字符串复合词应采用正确的大小写 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ResourceStringCompoundWordsShouldBeCasedCorrectly
- CA1701
helpviewer_keywords:
- CA1701
- ResourceStringCompoundWordsShouldBeCasedCorrectly
ms.assetid: 4ddbe09f-24b8-4c47-9373-a06f4487ca0d
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 38d8195baa540c2c212c71938b6266e28df49101
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65683067"
---
# <a name="ca1701-resource-string-compound-words-should-be-cased-correctly"></a>CA1701:资源字符串组合词应采用正确的大小写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果这两个部件的组合词识别由拼写字典，目的是使用两个单词。

 此外可以为用于拼写检查器的自定义字典添加组合词。 自定义字典中的单词不会导致冲突。 有关详细信息，请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)。

## <a name="related-rules"></a>相关的规则
 [CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

 [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>请参阅
 [大小写约定](https://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)[命名准则](https://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)
