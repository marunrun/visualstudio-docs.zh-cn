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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c5088fc04f4440260bdb9d3f040d99061c05d243
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72620333"
---
# <a name="advanced-search-operators-in-search-expressions"></a>搜索表达式中的高级搜索运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用高级搜索运算符，可以通过创建更复杂的搜索表达式来改进内容的搜索。 如下表所示，这些运算符可限制运行查询的上下文。

> [!WARNING]
> 输入的高级搜索运算符必须以冒号结尾并且逗号前不能有空格，这样搜索引擎才能识别这些运算符。

|要搜索|使用“管理”工作区中的“连接的管理组”|示例|结果|
|-------------------|---------|-------------|------------|
|主题标题中的字词|title:|title:binaryreader|标题中包含“binaryreader”的主题。|
|代码示例中的字词|code:|code:readdouble|代码示例中包含“readdouble”的的主题。|
|特定编程语言的一个示例中的字词|code:vb:|code:vb:string|Visual Basic 示例中包含“string”的主题。|
|与特定索引关键字关联的主题|keyword:|keyword:readbyte|与“readbyte”索引关键字关联的主题。|

 可使用 code: 运算符查找任意编程语言的相关内容，但它的返回结果仅包含标记为特定编程语言的内容。 下表列出了此运算符支持的编程语言：

|编程语言|使用“管理”工作区中的“连接的管理组”|
|--------------------------|---------|
|Visual Basic|code:vb<br /><br /> 或<br /><br /> code:visualbasic|
|C#|code:c#<br /><br /> 或<br /><br /> code:csharp|
|C++|code:cpp<br /><br /> 或<br /><br /> code:c++<br /><br /> 或<br /><br /> code:cplusplus|
|F#|code:f#<br /><br /> 或<br /><br /> code:fsharp|
|JavaScript|code:javascript<br /><br /> 或<br /><br /> code:js|
|XAML|code:xaml|

## <a name="see-also"></a>请参阅
 [搜索表达式中的逻辑运算符](../ide/logical-operators-in-search-expressions.md)[全文搜索提示](../ide/full-text-search-tips.md)
