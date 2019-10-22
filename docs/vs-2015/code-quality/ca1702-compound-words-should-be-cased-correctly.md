---
title: CA1702：复合词应采用正确的大小写 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
helpviewer_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
ms.assetid: 05481245-7ad8-48c3-a456-3aa44b6160a6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 76ce346430a249b562f00e17c3173e79128d1708
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669254"
---
# <a name="ca1702-compound-words-should-be-cased-correctly"></a>CA1702：复合词应采用正确的大小写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[CA1702：复合词应采用正确的大小写](https://docs.microsoft.com/visualstudio/code-quality/ca1702-compound-words-should-be-cased-correctly)。

|||
|-|-|
|TypeName|CompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1702|
|类别|Microsoft。命名|
|是否重大更改|重大-对程序集引发时。<br /><br /> 不间断-在类型参数上触发时。|

## <a name="cause"></a>原因
 标识符的名称包含多个字词，其中至少有一个单词显示为大小写不正确的组合词。

## <a name="rule-description"></a>规则说明
 标识符的名称拆分为基于大小写的单词。 Microsoft 拼写检查器库检查每个连续两个单词的组合。 如果识别，标识符将生成规则冲突。 导致冲突的组合词的示例包括 "CheckSum" 和 "多部分"，分别应以 "Checksum" 和 "多部分" 的大小写形式。 由于以前的常见用法，规则中内置了几个例外，并标记了几个单个字词（如 "Toolbar" 和 "Filename"），其大小写应为两个不同的单词（在本例中为 "ToolBar" 和 "FileName"）。

 命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突
 更改名称，使其大小写正确。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果拼写词典识别了复合单词的两个部分，并且目的是使用两个词，则可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
 [CA1701：资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

 [CA1709：标识符的大小写应当正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708：标识符不应仅以大小写进行区分](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>请参阅
 [命名准则](https://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)[大小写约定](https://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)
