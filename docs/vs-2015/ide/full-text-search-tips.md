---
title: 全文搜索提示 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- hv_search
helpviewer_keywords:
- Help Viewer 2.0, full-text search tips
- full-text search tips [Help Viewer 2.0]
ms.assetid: bcaad23d-2ca7-4bec-8b54-b884bc34e70b
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 686bf7962e164e718f007a44c83febfc8f49418d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62584678"
---
# <a name="full-text-search-tips"></a>全文搜索提示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在“帮助”中查找信息更为有用的方法之一是执行全文搜索。 若要修改和自定义结果，必须了解语法对查询的影响方式。 本主题提供提示、过程和详细的语法信息，帮助你更好地利用查询。  
  
## <a name="full-text-search-tips"></a>全文搜索提示  
 了解“帮助”如何解释查询格式后，可以让搜索目的性更强，在查询中仅返回你感兴趣的主题。 这些格式包括特殊字符、保留字和筛选器。  
  
### <a name="general-guidelines"></a>通用准则  
 下表包括在“帮助”中进行搜索查询的一些基本规则和指南。  
  
|语法|说明|  
|------------|-----------------|  
|区分大小写|搜索不区分大小写。 使用大写或小写字符设置搜索条件。 例如，“OLE”和“ole”返回相同的结果。|  
|字符组合|不能仅搜索单个字母 (a-z) 或单个数字 (0-9)。 如果尝试搜索某些保留字，如“and”、“from”和“with”，它们将被忽略。 有关详细信息，请参阅本主题后面部分的“搜索中忽略的字（停用字）”。|  
|计算顺序|搜索查询从左到右进行求值。|  
  
### <a name="search-syntax"></a>搜索语法  
 如果指定搜索包含多个单词（如“word1 word2”）的字符串，该字符串等效于键入“word1 AND word2”，将仅返回包含搜索字符串中各个单词的主题。  
  
> [!IMPORTANT]
> 1. 不支持短语搜索。 如果在搜索字符串中指定多个单词，返回的主题将包含所有指定的单词，但不一定是确切指定的短语。  
>    2. 使用逻辑运算符指定搜索短语中各单词之间的关系。 可以使用逻辑运算符（如 AND、OR NOT 和 NEAR）进一步优化搜索。 例如，如果搜索“declaring NEAR union”，搜索结果将包括包含“declaring”和“union”单词的主题，除这两个词之外，仅有几个单词。 有关详细信息，请参阅[搜索表达式中的逻辑运算符](../ide/logical-operators-in-search-expressions.md)。  
  
### <a name="filters"></a>筛选器  
 可利用高级搜索运算符进一步限制搜索结果。 “帮助”包括三类用于筛选全文搜索结果的方式：标题、代码和关键字。 有关详细信息，请参阅[搜索表达式中的高级搜索运算符](../ide/advanced-search-operators-in-search-expressions.md)。  
  
### <a name="ranking-of-search-results"></a>搜索结果的排名  
 搜索算法应用特定条件在结果列表中对搜索结果进行排名。 通常情况下：  
  
1. 标题中包含搜索词的内容排名高于标题中不包含搜索词的内容。  
  
2. 搜索词紧挨的内容高于搜索词较远的内容。  
  
3. 包含较多搜索词的内容排名高于包含较少搜索词的内容。  
  
### <a name="words-ignored-in-searches-stop-words"></a>搜索中忽略的字（停用字）  
 全文索引搜索期间，会自动忽略经常出现的单词或数字（有时也称停用字）。 例如，如果搜索短语“pass through”，搜索结果将显示包含“pass”而非“through”的主题。  
  
## <a name="see-also"></a>请参阅  
 [查找信息](../ide/locate-information.md)   
 [搜索表达式中的逻辑运算符](../ide/logical-operators-in-search-expressions.md)
