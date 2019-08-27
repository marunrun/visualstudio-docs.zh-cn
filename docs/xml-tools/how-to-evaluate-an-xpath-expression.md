---
title: 计算 XPath 表达式在调试时
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1585b54d084e3471583f9388d63f5c17e65fc3a7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63002086"
---
# <a name="evaluate-xpath-expressions"></a>计算 XPath 表达式

可以通过使用计算 XPath 表达式**快速监视**窗口在调试过程中的。 XPath 表达式必须符合 W3C XPath 1.0 建议。 当前 XSLT 上下文 (即`self::node()`中的节点**局部变量**窗口) 为 XPath 表达式提供计算上下文。

当计算 XPath 表达式：

- 支持内置 XPath 函数。

- 不支持内置 XSLT 函数和用户定义的函数。

> [!NOTE]
> XSLT 调试是仅在 Visual Studio Enterprise edition 中可用。

## <a name="evaluate-an-xpath-expression"></a>评估 XPath 表达式

以下过程使用*average.xsl 下面*并*books.xml*文件从[演练：调试 XSLT 样式表](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md#sample-files)页。

1. 在 `xsl:if` 开始标记处插入断点。

2. 若要开始调试，请选择**XML** > **启动 XSLT 调试**在菜单栏上 (或按**Alt**+**F5**).

   调试程序在 `xsl:if` 标记处开始和中断。

3. 右键单击并选择**快速监视**。

   **快速监视**窗口随即打开。

4. 输入`./price/text()`中**表达式**字段**快速监视**对话框框中，，然后选择**重新评估**。

   当前 book 节点的价格将出现在**值**框。

   ![计算 XPath 表达式中的快速监视窗口](media/quickwatch-price.png)

5. 将 XPath 表达式更改为`./price/text() < $bookAverage`然后单击**重新评估**。

   **值**框中显示的 XPath 表达式计算结果为`true`。

## <a name="see-also"></a>请参阅

- [调试 XSLT](../xml-tools/debugging-xslt.md)