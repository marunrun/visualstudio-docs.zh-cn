---
title: CA1703：资源字符串应正确拼写 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ResourceStringsShouldBeSpelledCorrectly
- CA1703
helpviewer_keywords:
- CA1703
- ResourceStringsShouldBeSpelledCorrectly
ms.assetid: 693f4970-f512-40cb-ae3b-a0f3a5c6d6f1
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9574ff022e0d5407b2683e5ba7a6b2e0cde5201e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669223"
---
# <a name="ca1703-resource-strings-should-be-spelled-correctly"></a>CA1703：资源字符串应正确拼写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ResourceStringsShouldBeSpelledCorrectly|
|CheckId|CA1703|
|类别|Microsoft。命名|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 资源字符串包含一个或多个未被 Microsoft 拼写检查器库识别的单词。

## <a name="rule-description"></a>规则说明
 此规则将资源字符串分析为单词（词汇切分组合词），并检查每个单词/标记的拼写。 有关分析算法的信息，请参阅[CA1704：标识符应拼写正确](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

 默认情况下，使用英语（en）版本的拼写检查器。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用拼写正确的完整单词，或将单词添加到自定义字典中。 有关如何使用自定义字典的信息，请参阅[CA1704：标识符应拼写正确](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 拼写正确的单词可减少学习新软件库所需的时间。

## <a name="related-rules"></a>相关规则
 [CA1701：资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

 [CA1704：标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

 [CA2204：应正确拼写文本](../code-quality/ca2204-literals-should-be-spelled-correctly.md)
