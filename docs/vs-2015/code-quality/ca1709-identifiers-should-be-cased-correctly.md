---
title: CA1709:标识符应采用正确的大小写 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldBeCasedCorrectly
- CA1709
helpviewer_keywords:
- CA1709
- IdentifiersShouldBeCasedCorrectly
ms.assetid: f633d1a7-4ca4-40ae-b207-ec571c5fb083
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b447b111cedc30aa23f3aaad0fbc964a5d8a2bd2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189163"
---
# <a name="ca1709-identifiers-should-be-cased-correctly"></a>CA1709:标识符的大小写应当正确
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[CA1709:标识符应采用正确的大小写](https://docs.microsoft.com/visualstudio/code-quality/ca1709-identifiers-should-be-cased-correctly)。  
  
|||  
|-|-|  
|TypeName|IdentifiersShouldBeCasedCorrectly|  
|CheckId|CA1709|  
|类别|Microsoft.Naming|  
|是否重大更改|-时中断程序集、 命名空间、 类型、 成员和参数的方法引发。<br /><br /> 无间断-触发泛型类型参数上时。|  
  
## <a name="cause"></a>原因  
 标识符名称的大小写不正确。  
  
 \- 或 -  
  
 标识符名称包含两个字母缩写词和第二个字母为小写形式。  
  
 \- 或 -  
  
 标识符名称包含三个或多个大写字母的首字母缩写。  
  
## <a name="rule-description"></a>规则说明  
 命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。  
  
 按照约定，参数名称使用驼峰式大小写;命名空间、 类型和成员名称使用 Pascal 大小写。 Camel 大小写的名称，第一个字母为小写，并在名称中的其他所有单词的第一个字母为大写。 Camel 大小写名称的示例是"packetSniffer"、"ioFile"和"fatalErrorCode"。 Pascal 大小写的名称中的第一个字母为大写，并在名称中的其他所有单词的第一个字母为大写。 Pascal 大小写名称的示例是"PacketSniffer"、"IOFile"和"FatalErrorCode"。  
  
 此规则将名称拆分成单词根据大小写，并检查任何两个字母的词与一系列常见的两个字母单词，如"In"或"My"。 如果找不到匹配项，单词被假定为首字母缩写词。 此外，此规则假定它找到一个缩写词时名称包含在行中的四个大写字母或名称的末尾处的行中的三个大写字母。  
  
 按照约定，两字母缩写词使用全大写字母和首字母缩写词的三个或多个字符使用 Pascal 大小写。 下面的示例使用此命名约定：'DB'、 CR、 Cpa 和 Ecma。 下面的示例违反约定：Io'、 'XML' 和 'DoD，以及用于 nonparameter 名称、 xp 和 cpl。  
  
 ID 是特殊情况，若要使此规则的冲突。 “Id”不是首字母缩略词，而是“identification”的缩写。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 更改名称，使其具有正确的大小写。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 它可以安全地禁止显示此警告，如果有自己的命名约定，或者如果标识符表示正确的名称，例如，一家公司或一种技术的名称。  
  
 您还可以添加特定的字词、 缩写和首字母缩写词给代码分析自定义字典。 指定自定义字典中的字词不会导致违反此规则。 有关详细信息，请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)  
  
## <a name="related-rules"></a>相关的规则  
 [CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
