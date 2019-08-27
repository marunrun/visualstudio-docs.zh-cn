---
title: CA1702:复合词应采用正确的大小写 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 91a3945c6ef212ba664119a822123f326cdefc5c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65676391"
---
# <a name="ca1702-compound-words-should-be-cased-correctly"></a>CA1702:组合词应采用正确的大小写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[CA1702:复合词应采用正确的大小写](https://docs.microsoft.com/visualstudio/code-quality/ca1702-compound-words-should-be-cased-correctly)。  
  
|||  
|-|-|  
|TypeName|CompoundWordsShouldBeCasedCorrectly|  
|CheckId|CA1702|  
|类别|Microsoft.Naming|  
|是否重大更改|对程序集引发重大时。<br /><br /> 无间断-如果在类型参数上引发。|  
  
## <a name="cause"></a>原因  
 标识符名称包含多个单词和至少一个单词似乎是大小写不正确的组合词。  
  
## <a name="rule-description"></a>规则说明  
 标识符名称拆分为根据大小写的单词。 通过 Microsoft 拼写检查器库会检查每个连续的两个单词组合。 如果它被识别，该标识符将生成与规则的冲突。 复合词而导致违反了示例包括"CheckSum"和"多部分"应采用的大小写为"Checksum"和"多部分"，分别。 由于以前经常使用，几个例外情况内置规则，并标记了几个单个单词，例如"工具栏"和"Filename"，，应采用的大小写为两个不同的单词 （在此情况下，"工具栏"和"FileName"）。  
  
 命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 更改名称，使其具有正确的大小写。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 它可以安全地禁止显示此规则的警告，如果这两个部件的组合词识别由拼写字典，目的是使用两个单词。  
  
## <a name="related-rules"></a>相关的规则  
 [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)  
  
 [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)  
  
 [CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)  
  
## <a name="see-also"></a>请参阅  
 [命名准则](https://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)   
 [大小写约定](https://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)
