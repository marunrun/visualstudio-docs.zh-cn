---
title: 调试时评估 XPath 表达式
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2e0b6c84fa9447dc38aa7976fa59bb5aa67d5c3
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592719"
---
# <a name="evaluate-xpath-expressions"></a>评估 XPath 表达式

在调试过程中，你可以使用“快速监视”窗口来评估 XPath 表达式。 XPath 表达式必须符合 W3C XPath 1.0 建议。 当前 XSLT 上下文（即“局部变量”窗口中的 `self::node()` 节点）为 XPath 表达式提供评估上下文。

评估 XPath 表达式时：

- 支持内置 XPath 函数。

- 不支持内置 XSLT 函数和用户定义的函数。

> [!NOTE]
> XSLT 调试仅适用于 Visual Studio 企业版。

## <a name="evaluate-an-xpath-expression"></a>评估 XPath 表达式

以下步骤使用[演练： 调试 XSLT 样式表](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md#sample-files)页中的 below-average.xsl 和 books.xml 文件。

1. 在 `xsl:if` 开始标记处插入断点。

2. 若要启动调试，请在菜单栏上选择“XML” > “启动 XSLT 调试”（或按 Alt+F5）   。

   调试程序在 `xsl:if` 标记处开始和中断。

3. 右键单击并选择“快速监视”。

   “快速监视”窗口随即打开。

4. 在“快速监视”对话框的“表达式”字段中，输入 `./price/text()`，然后选择“重新评估”  。

   当前 book 节点的价格将出现在“值”框中。

   ![在“快速监视”窗口中评估 XPath 表达式](media/quickwatch-price.png)

5. 将 XPath 表达式更改为 `./price/text() < $bookAverage`，然后单击“重新评估”。

   “值”框显示 XPath 表达式的评估结果为 `true`。

## <a name="see-also"></a>请参阅

- [调试 XSLT](../xml-tools/debugging-xslt.md)
