---
title: CA2204：应正确拼写文本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Literals should be spelled correctly
- CA2204
- LiteralsShouldBeSpelledCorrectly
helpviewer_keywords:
- CA2204
ms.assetid: b0bbcbb6-c92d-4c14-8ef7-9c8b38c791a6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ecf829251cbeab600cb95f8f0c0b0173cd7338d4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546271"
---
# <a name="ca2204-literals-should-be-spelled-correctly"></a>CA2204:文字应正确拼写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|LiteralsShouldBeSpelledCorrectly|
|CheckId|CA2204|
|Category|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 方法将字符串传递到一个参数或属性中使用的字符串，该字符串需要本地化字符串并且文本字符串包含 Microsoft 拼写检查器库无法识别的一个或多个字词。

## <a name="rule-description"></a>规则描述
 如果以下一个或多个条件为 true，则此规则将检查作为值传递到参数或属性的文本字符串：

- <xref:System.ComponentModel.LocalizableAttribute>参数或属性的属性设置为 true。

- 参数或属性名称包含 "文本"、"消息" 或 "标题"。

- 传递给控制台. Write 或 Console 方法的字符串参数的名称为 "value" 或 "format"。

  此规则将文本字符串分析为单词词汇切分，并检查每个单词/标记的拼写。 有关分析算法的信息，请参阅[CA1704：标识符应拼写正确](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

  默认情况下，使用英语（en）版本的拼写检查器。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请更正单词的拼写，或将该词添加到自定义字典中。 有关如何使用自定义字典的信息，请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 拼写正确的单词减少了新软件库所需的学习曲线。

## <a name="related-rules"></a>相关规则
 [CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

 [CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
