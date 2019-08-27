---
title: 如何：计算 XPath 表达式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 03c43d272d3c740c55314db5d1b7b6c225b7e5c8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63421760"
---
# <a name="how-to-evaluate-an-xpath-expression"></a>如何：计算 XPath 表达式
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用计算 XPath 表达式**快速监视**对话框。 XPath 表达式必须符合 W3C XPath 1.0 建议。 当前 XSLT 上下文 — 即，`self::node()`中的节点**局部变量**窗口 — 为 XPath 表达式提供计算上下文。  
  
 下表说明在计算 XPath 表达式时支持的函数：  
  
- 支持内置 XPath 函数。  
  
- 不支持内置 XSLT 函数。  
  
- 不支持用户定义函数。  
  
> [!NOTE]
> 以下过程使用的 belowAvg.xsl 和 books.xml 文件[演练：调试 XSLT 样式表](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)主题。  
  
### <a name="to-evaluate-an-xpath-expression"></a>计算 XPath 表达式  
  
1. 在 `xsl:if` 开始标记处插入断点。  
  
2. 单击**调试 XSL** XML 编辑器工具栏上的按钮。  
  
     调试程序在 `xsl:if` 标记处开始和中断。  
  
3. 右键单击并选择**快速监视**。  
  
     **快速监视**显示对话框。  
  
4. 输入`./price/text()`中**表达式**字段**快速监视**对话框中，单击**重新评估**。  
  
     当前 book 节点的价格将出现在**值**框。  
  
5. 将 XPath 表达式更改为`./price/text() < $bookAverage`然后单击**重新评估**。  
  
     **值**框中显示的 XPath 表达式计算结果为`true`。  
  
## <a name="see-also"></a>请参阅  
 [调试 XSLT](../xml-tools/debugging-xslt.md)
