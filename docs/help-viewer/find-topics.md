---
title: 搜索主题（帮助查看器）
ms.date: 11/02/2017
ms.topic: conceptual
ms.assetid: 683f1b0c-1551-4bba-91fe-3855f03fdd69
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 52818e4f676d6ae9f4c02f26ad8e354b206cb2b8
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824996"
---
# <a name="how-to-search-for-topics"></a>如何：搜索主题

可以使用全文搜索功能找到包含特定单词的所有主题。 还可以通过使用通配符表达式、逻辑运算符和高级搜索运算符优化与自定义搜索。

若要打开“搜索”选项卡，请选择“帮助查看器”窗口中的“搜索”选项卡；如果是键盘用户，则选择 Ctrl+E      。

## <a name="to-perform-a-full-text-search"></a>执行全文搜索

1. 在搜索框中，键入要查找的单词。

2. 在搜索查询中，指定要应用于搜索的逻辑或高级搜索运算符（如果有）。 若要搜索所有可用帮助，请勿使用运算符。

    > [!NOTE]
    > 在“Viewer 选项”  对话框中，可以指定附加首选项，比如一次显示的搜索结果最大数量，以及主要区域设置不是英语时是否包含英语内容。

3. 选择 **Enter** 键。

     默认情况下，一次搜索最多返回 200 个命中结果，并显示在搜索结果区域中。 每个结果的附加版本信息可能会根据内容显示。

4. 若要查看主题，请从结果列表中选择其标题。

## <a name="full-text-search-tips"></a>全文搜索提示

了解语法对查询的影响后，可以让搜索目的性更强，仅返回你感兴趣的主题。 语法包括特殊字符、保留字和筛选器。 本主题提供提示、过程和详细的语法信息，帮助你更好地利用查询。

### <a name="general-guidelines"></a>通用准则

下表包括在帮助中进行搜索查询的一些基本规则和指南。

|语法|说明|
|------------|-----------------|
|区分大小写|搜索不区分大小写。 使用大写或小写字符设置搜索条件。 例如，“OLE”和“ole”返回相同的结果。|
|字符组合|不能仅搜索单个字母 (a-z) 或单个数字 (0-9)。 如果尝试搜索某些保留字，如“and”、“from”和“with”，它们将被忽略。 有关详细信息，请参阅本主题后面的[搜索中忽略的字](#stopwords)。|
|计算顺序|搜索查询从左到右进行求值。|

### <a name="search-syntax"></a>搜索语法

如果指定搜索包含多个单词（如“word1 word2”）的字符串，该字符串等效于键入“word1 AND word2”，将仅返回包含搜索字符串中各个单词的主题。

> [!IMPORTANT]
> - 不支持短语搜索。 如果在搜索字符串中指定多个单词，返回的主题将包含所有指定的单词，但不一定是确切指定的短语。
> - 使用逻辑运算符指定搜索短语中各单词之间的关系。 可以使用逻辑运算符（如 AND、OR NOT 和 NEAR）进一步优化搜索。 例如，如果搜索“declaring NEAR union”，搜索结果将包括包含“declaring”和“union”单词的主题，除这两个词之外，仅有几个单词。 有关详细信息，请参阅[搜索表达式中的逻辑运算符](../help-viewer/logical-operators-search-expressions.md)。

### <a name="filters"></a>筛选器

可利用高级搜索运算符进一步限制搜索结果。 “帮助”包括三个可用于筛选全文搜索结果的类别：“标题”、“代码”和“关键字”。

### <a name="ranking-of-search-results"></a>搜索结果排名

搜索算法应用特定条件在结果列表中对搜索结果进行排名。 通常情况下：

1. 标题中包含搜索词的内容排名高于标题中不包含搜索词的内容。

2. 搜索词紧挨的内容高于搜索词较远的内容。

3. 包含较多搜索词的内容排名高于包含较少搜索词的内容。

### <a name="stopwords">搜索中忽略的字（停用字）</a>

全文索引搜索期间，会自动忽略经常出现的单词或数字（有时也称停用字）。 例如，如果搜索短语“pass through”，搜索结果将显示包含“pass”而非“through”的主题。

## <a name="see-also"></a>请参阅

- [逻辑运算符和高级运算符](../help-viewer/logical-operators-search-expressions.md)
- [如何：在索引中查找主题](../help-viewer/find-topics-index.md)
- [如何：在 TOC 中查找主题](../help-viewer/find-topics-toc.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)