---
title: 搜索表达式中的逻辑运算符/高级运算符（帮助查看器）
ms.date: 11/02/2017
ms.topic: reference
helpviewer_keywords:
- Help Viewer, logical operators in search
- logical operators in search [Help Viewer]
ms.assetid: 0c38ae7d-3e20-4d47-a020-9677cd285916
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0e241df6c32fc1b0a8e88942fe5d0d178c37b9bf
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824901"
---
# <a name="logical-and-advanced-operators-in-search-expressions"></a>搜索表达式中的逻辑和高级运算符

可以在 Help Viewer 中使用逻辑运算符和高级搜索运算符优化帮助内容的搜索  。

## <a name="logical-operators"></a>逻辑运算符

逻辑运算符指定在搜索查询中组合多个搜索词的方式。 下表显示了逻辑运算符 AND、OR、NOT 和 NEAR。

|要搜索|使用|示例|结果|
|-------------------|---------|-------------|------------|
|同一文章中的两个词|AND|dib AND palette|包含“dib”和“palette”的主题。|
|文章中的任一个词|或|raster OR vector|包含“raster”或“vector”的主题|
|同一文章中包含第一个词，而不包含第二个词|NOT|"operating system" NOT DOS|包含“operating system”但不包含“DOS”的主题。|
|文章中两个词相互靠近|相邻|user NEAR kernel|包含与“kernel”靠近的“user”的主题。|

> [!IMPORTANT]
> 必须使用全部大写字母的格式输入逻辑运算符，以便搜索引擎可以识别它们。

## <a name="advanced-operators"></a>高级运算符

高级搜索运算符可指定在文章中的哪个位置查找搜索词，从而优化内容搜索。 下表介绍了四个可用的高级搜索运算符。

|要搜索|使用|示例|结果|
|-------------------|---------|-------------|------------|
|文章标题中的字词|`title:`|`title:binaryreader`|标题中包含“binaryreader”的主题。|
|代码示例中的字词|`code:`|`code:readdouble`|代码示例中包含“readdouble”的的主题。|
|特定编程语言的一个示例中的字词|`code:vb:`|`code:vb:string`|Visual Basic 代码示例中包含“string”的主题。|
|与特定索引关键字关联的文章|`keyword:`|`keyword:readbyte`|与“readbyte”索引关键字关联的主题。|

> [!IMPORTANT]
> 输入的高级搜索运算符必须以冒号结尾并且逗号前不能有空格，这样搜索引擎才能识别这些运算符。

### <a name="programming-languages-for-code-examples"></a>代码示例的编程语言

可以使用 `code:` 运算符查找若干编程语言中任意一种语言的相关内容。 若要返回特定编程语言的示例，请使用以下编程语言值之一：

|编程语言|搜索运算符语法|
| - |---------|
|Visual Basic|`code:vb`<br/>`code:visualbasic`|
|C#|`code:c#`<br/>`code:csharp`|
|C++|`code:cpp`<br/>`code:c++`<br/>`code:cplusplus`|
|F#|`code:f#`<br/>`code:fsharp`|
|JavaScript|`code:javascript`<br/>`code:js`|
|XAML|`code:xaml`|

> [!NOTE]
> `code:` 运算符仅查找标记有编程语言标签的内容，而不查找一般标记为代码的内容。

## <a name="see-also"></a>请参阅

- [如何：搜索主题](../help-viewer/find-topics.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)
