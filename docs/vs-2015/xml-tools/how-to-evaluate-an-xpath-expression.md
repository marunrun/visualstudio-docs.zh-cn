---
title: 如何：计算 XPath 表达式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ecec9004506a9bd05d3d773e44bb264af363f96f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670867"
---
# <a name="how-to-evaluate-an-xpath-expression"></a>如何：计算 XPath 表达式
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过 "**快速监视**" 对话框计算 XPath 表达式。 XPath 表达式必须符合 W3C XPath 1.0 建议。 当前 XSLT 上下文—即 "**局部变量**" 窗口中的 "`self::node()`" 节点—为 XPath 表达式提供计算上下文。

 下表说明在计算 XPath 表达式时支持的函数：

- 支持内置 XPath 函数。

- 不支持内置 XSLT 函数。

- 不支持用户定义函数。

> [!NOTE]
> 下面的过程使用 "[演练：调试 XSLT 样式表](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)" 主题中的 belowavg.xsl 和 books.xml 文件。

### <a name="to-evaluate-an-xpath-expression"></a>计算 XPath 表达式

1. 在 `xsl:if` 开始标记处插入断点。

2. 单击 "XML 编辑器" 工具栏上的 "**调试 XSL** " 按钮。

     调试程序在 `xsl:if` 标记处开始和中断。

3. 右键单击并选择 "**快速监视**"。

     随即显示 "**快速监视**" 对话框。

4. 在 "**快速监视**" 对话框的 "**表达式**" 字段中输入 `./price/text()`，并单击 "重新**计算**"。

     当前 book 节点的价格显示在 "**值**" 框中。

5. 将 XPath 表达式更改为 "`./price/text() < $bookAverage`"，然后单击 "重新**计算**"。

     "**值**" 框显示 XPath 表达式的计算结果为 `true`。

## <a name="see-also"></a>请参阅
 [调试 XSLT](../xml-tools/debugging-xslt.md)
