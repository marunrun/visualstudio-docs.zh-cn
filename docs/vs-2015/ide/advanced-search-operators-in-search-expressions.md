---
title: 搜索表达式中的高级搜索运算符 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Help Viewer 2.0, searching for keywords
- Help Viewer 2.0, searching code
- Help Viewer 2.0, searching code by programming language
- Help Viewer 2.0, searching titles
- searching code [Help Viewer 2.0]
- searching titles [Help Viewer 2.0]
ms.assetid: 0cdc1746-8481-45ec-9c53-d0d89cdcbd5e
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6befa20bcda7f30896fb2b04fadefb0eb5f21f8d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63408410"
---
# <a name="advanced-search-operators-in-search-expressions"></a>搜索表达式中的高级搜索运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用高级的搜索运算符，您可以通过创建更复杂的搜索表达式较简单的优化内容搜索。 如下表所示，这些运算符可限制运行查询的上下文。  
  
> [!WARNING]
> 输入的高级搜索运算符必须以冒号结尾并且逗号前不能有空格，这样搜索引擎才能识别这些运算符。  
  
|要搜索|使用|示例|结果|  
|-------------------|---------|-------------|------------|  
|主题标题中的字词|title:|title:binaryreader|标题中包含“binaryreader”的主题。|  
|代码示例中的字词|code:|code:readdouble|代码示例中包含“readdouble”的的主题。|  
|特定编程语言的一个示例中的字词|code:vb:|code:vb:string|Visual Basic 示例中包含“string”的主题。|  
|与特定索引关键字关联的主题|keyword:|keyword:readbyte|与“readbyte”索引关键字关联的主题。|  
  
 可使用 code: 运算符查找任意编程语言的相关内容，但它的返回结果仅包含标记为特定编程语言的内容。 下表列出了此运算符支持的编程语言：  
  
|编程语言|使用|  
|--------------------------|---------|  
|Visual Basic|code:vb<br /><br /> 或<br /><br /> code:visualbasic|  
|C#|code:c#<br /><br /> 或<br /><br /> code:csharp|  
|C++|code:cpp<br /><br /> 或<br /><br /> code:c++<br /><br /> 或<br /><br /> code:cplusplus|  
|F#|code:f#<br /><br /> 或<br /><br /> code:fsharp|  
|JavaScript|code:javascript<br /><br /> 或<br /><br /> code:js|  
|XAML|code:xaml|  
  
## <a name="see-also"></a>请参阅  
 [搜索表达式中的逻辑运算符](../ide/logical-operators-in-search-expressions.md)   
 [全文搜索提示](../ide/full-text-search-tips.md)
