---
title: CA1701：资源字符串复合词应采用正确的大小写 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7c1c3b0fd6cf3a25d5db9e3039d4dc5d8364a18e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544100"
---
# <a name="ca1701-resource-string-compound-words-should-be-cased-correctly"></a>CA1701:资源字符串组合词应采用正确的大小写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ResourceStringCompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1701|
|Category|Microsoft。命名|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 资源字符串包含的复合单词的大小写不正确。

## <a name="rule-description"></a>规则描述
 资源字符串中的每个单词都拆分为基于大小写的标记。 Microsoft 拼写检查器库会对由两个连续的标记构成的每个组合进行检查。 如果被识别，该单词将生成规则冲突。 导致冲突的组合词的示例包括 "CheckSum" 和 "多部分"，分别应以 "Checksum" 和 "多部分" 的大小写形式。 由于以前的常见用法，规则中内置了几个例外，并标记了几个单个字词（如 "Toolbar" 和 "Filename"），其大小写应为两个不同的单词。 在此示例中，将标记 "工具栏" 和 "文件名"。

 命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突
 更改单词，使其大小写正确。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果拼写词典识别了复合单词的两个部分，并且目的是使用两个词，则可以安全地禁止显示此规则发出的警告。

 还可以向拼写检查器的自定义字典中添加复合单词。 自定义字典中的单词不会导致冲突。 有关详细信息，请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)。

## <a name="related-rules"></a>相关规则
 [CA1702:组合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

 [CA1709:标识符的大小写应当正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:标识符应以大小写之外的差别进行区分](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>另请参阅
 [大小写约定](https://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)[命名准则](https://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)
