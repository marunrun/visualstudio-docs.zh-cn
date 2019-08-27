---
title: 调试 XSLT 样式表
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e787ca3d2d29f04d6af27a5f36f1f84c9d0bc9f4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808461"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>演练：调试 XSLT 样式表

此演练中的步骤演示如何使用 XSLT 调试程序。 步骤包括查看变量、设置断点和逐行执行代码。 调试程序，可一次执行一行代码。

若要准备此演练，请首先将复制这两个[示例文件](#sample-files)到本地计算机。 一个样式表，其中一个是 XML 文件，我们将使用作为输入的样式表。 在此演练中，我们使用的样式表查找所有它的成本低于平均书价的书籍。

> [!NOTE]
> XSLT 调试程序是仅在 Visual Studio Enterprise edition 中可用。

## <a name="start-debugging"></a>“启动调试”

1. 从**文件**菜单中，选择**打开** > **文件**。

2. 找到*average.xsl 下面*文件，然后选择**打开**。

   在 XML 编辑器中打开样式表。

3. 单击浏览按钮 (**...**) 上**输入**字段的文档属性窗口。 (如果**属性**窗口不可见，右键单击编辑器中打开的文件的任意位置，然后选择**属性**。)

4. 找到*books.xml*文件，，然后选择**打开**。

   此设置用于 XSLT 转换的源文档文件。

5. 设置[断点](../debugger/using-breakpoints.md)在第 12 个行*如下 average.xsl*。 你可以通过多种方式之一：

   - 在第 12 行编辑器边距中单击。

   - 单击第 12 行上的任意位置，然后按**F9**。

   - 右键单击`xsl:if`开始标记处，，然后选择**断点** > **插入断点**。

      ![在 Visual Studio 中的 XSL 文件中插入断点](media/insert-breakpoint.PNG)

6. 在菜单栏上依次选择**XML** > **启动 XSLT 调试**(或按**Alt**+**F5**)。

   在调试过程开始。

   在编辑器中，调试器位于上`xsl:if`元素的样式表。 另一个名为的文件*average.xml 下面*编辑器; 中打开这是将填充为输入文件中的每个节点的输出文件*books.xml*进行处理。

   **自动**，**局部变量**，并**监视 1** windows 显示在 Visual Studio 窗口的底部。 **局部变量**窗口显示所有局部变量及其当前值。 其中包括样式表中定义的变量，也包括调试程序在跟踪上下文中的当前节点时使用的变量。

## <a name="watch-window"></a>监视窗口

我们将添加到两个变量**监视 1**窗口，使我们可以在处理输入的文件时检查它们的值。 (还可以使用**局部变量**窗口来检查值，如果您想要监视的变量已存在。)

1. 从**调试**菜单中，选择**Windows** > **监视** > **监视 1**。

   **监视 1**窗口变得可见。

2. 类型`$bookAverage`中**名称**字段中，，然后按**Enter**。

   值`$bookAverage`变量显示在**值**字段。

3. 在下一步的行中键入`self::node()`中**名称**字段中，，然后按**Enter**。

   `self::node()` 是一个计算结果为当前上下文节点的 XPath 表达式。 `self::node()` XPath 表达式的值是第一个 book 节点。 此值随着转换的进度而更改。

4. 展开`self::node()`节点，然后展开节点谁具有值为`price`。

   ![在 Visual Studio 中调试 XSLT 监视窗口](media/xslt-debugging-watch-window.png)

   您可以查看当前 book 节点的书价的值并将对其进行比较`$bookAverage`值。 因为书价低于平均值，`xsl:if`条件应成立时继续调试过程。

## <a name="step-through-the-code"></a>单步执行代码

1. 按 F5 继续。

   因为第一个 book 节点满足`xsl:if`条件，book 节点将添加到*如下 average.xml*输出文件。 调试器继续执行，直到它再次位于样式表中的 `xsl:if` 元素上。 调试器此时位于上的第二个 book 节点中*books.xml*文件。

   在中**监视 1**窗口中，`self::node()`值更改为第二个 book 节点。 通过检查 price 元素的值，可以确定价格高于平均值，所以，`xsl:if` 条件应失败。

2. 按 F5 继续。

   因为第二个 book 节点不满足`xsl:if`条件，不添加到 book 节点*如下 average.xml*输出文件。 调试器继续执行，直到它再次位于上`xsl:if`样式表中的元素。 调试器此时位于第三次`book`中的节点*books.xml*文件。

   在中**监视 1**窗口中，`self::node()`值更改为第三个 book 节点。 通过检查的值`price`元素中，您可以确定价格低于平均值。 `xsl:if`条件应成立。

3. 按 F5 继续。

   因为`xsl:if`满足条件时，第三个丛书将添加到*如下 average.xml*输出文件。 XML 文档中的所有 book 节点均已处理，调试程序停止。

## <a name="sample-files"></a>示例文件

下列两个文件供该演练使用。

### <a name="below-averagexsl"></a>below-average.xsl

```xml
<?xml version='1.0'?>
<xsl:stylesheet version="1.0"
      xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="xml" encoding="utf-8"/>
  <xsl:template match="/">
    <xsl:variable name="bookCount" select="count(/bookstore/book)"/>
    <xsl:variable name="bookTotal" select="sum(/bookstore/book/price)"/>
    <xsl:variable name="bookAverage" select="$bookTotal div $bookCount"/>
    <books>
      <!--Books That Cost Below Average-->
      <xsl:for-each select="/bookstore/book">
        <xsl:if test="price &lt; $bookAverage">
          <xsl:copy-of select="."/>
        </xsl:if>
      </xsl:for-each>
    </books>
  </xsl:template>
</xsl:stylesheet>
```

### <a name="booksxml"></a>books.xml

```xml
<?xml version='1.0'?>
<!-- This file represents a fragment of a book store inventory database -->
<bookstore>
  <book genre="autobiography" publicationdate="1981" ISBN="1-861003-11-0">
    <title>The Autobiography of Benjamin Franklin</title>
    <author>
      <first-name>Benjamin</first-name>
      <last-name>Franklin</last-name>
    </author>
    <price>8.99</price>
  </book>
  <book genre="novel" publicationdate="1967" ISBN="0-201-63361-2">
    <title>The Confidence Man</title>
    <author>
      <first-name>Herman</first-name>
      <last-name>Melville</last-name>
    </author>
    <price>11.99</price>
  </book>
  <book genre="philosophy" publicationdate="1991" ISBN="1-861001-57-6">
    <title>The Gorgias</title>
    <author>
      <name>Plato</name>
    </author>
    <price>9.99</price>
  </book>
</bookstore>
```

## <a name="see-also"></a>请参阅

- [调试 XSLT](../xml-tools/debugging-xslt.md)