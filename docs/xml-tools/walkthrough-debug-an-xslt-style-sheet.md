---
title: 调试 XSLT 样式表
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd5882cc606bf241a281940464ba028e77986807
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79300941"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>演练：调试 XSLT 样式表

此演练中的步骤演示如何使用 XSLT 调试程序。 步骤包括查看变量、设置断点和逐行执行代码。 调试器允许您一次执行一行代码。

为准备本演练，请先将两个[示例文件](#sample-files)复制到本地计算机。 一个是样式表，一个是我们将用作样式表输入的 XML 文件。 在本演练中，我们使用的样式表可查找所有成本低于平均书本价格的书籍。

> [!NOTE]
> XSLT 调试器仅在 Visual Studio 的企业版中可用。

## <a name="start-debugging"></a>开始调试

1. 在 **"文件"** 菜单中，选择 **"打开** > **文件**"。

2. 找到*低于平均水平.xsl*的文件，然后选择 **"打开**"。

   样式表将在 XML 编辑器中打开。

3. 单击文档属性窗口的 **"输入"** 字段上的浏览按钮 （**...）。** （如果 **"属性"** 窗口不可见，请右键单击编辑器中打开文件上的任意位置，然后选择 **"属性**"。"

4. 找到*book.xml*文件，然后选择 **"打开**"。

   这将设置用于 XSLT 转换的源文档文件。

5. 在*低于平均值.xsl*的第 12 行设置[断点](../debugger/using-breakpoints.md)。 您可以通过多种方式之一执行此操作：

   - 单击第 12 行编辑器的边距。

   - 单击第 12 行的任意位置，然后按**F9**。

   - 右键单击`xsl:if`起始标记，然后选择"**插入断点** > **Insert Breakpoint**"。

      ![在可视化工作室中的 XSL 文件中插入断点](media/insert-breakpoint.PNG)

6. 在菜单栏上，选择**XML** > **启动 XSLT 调试**（或者，按**Alt**+**F5**）。

   调试过程开始。

   在编辑器中，调试器位于样式表`xsl:if`的元素上。 另一个名为*低于平均值.xml*的文件将在编辑器中打开;这是将填充为输入文件*书.xml*中的每个节点的输出文件。

   **"自动**"、**局部变量**和**监视 1**窗口显示在可视化工作室窗口的底部。 **"局部变量"** 窗口显示所有局部变量及其当前值。 其中包括样式表中定义的变量，也包括调试程序在跟踪上下文中的当前节点时使用的变量。

## <a name="watch-window"></a>监视窗口

我们将向**Watch 1**窗口添加两个变量，以便在处理输入文件时检查它们的值。 （如果要查看的变量已存在，也可以使用 **"局部变量"** 窗口检查值。

1. 在**调试**菜单中，选择**Windows** > **监视** > **1**。

   **"监视 1"** 窗口变得可见。

2. 键入`$bookAverage`**"名称"** 字段，**然后按**Enter 。

   `$bookAverage`变量的值显示在 **"值"** 字段中。

3. 在下一行中，键入`self::node()`**"名称"** 字段，**然后按**Enter 。

   `self::node()`是一个 XPath 表达式，用于计算到当前上下文节点。 `self::node()` XPath 表达式的值是第一个 book 节点。 此值随着转换的进度而更改。

4. 展开`self::node()`节点，然后展开值为 的节点`price`。

   ![在可视化工作室中 XSLT 调试期间监视窗口](media/xslt-debugging-watch-window.png)

   您可以看到当前书籍节点的图书价格值，并将其与`$bookAverage`该值进行比较。 由于帐面价格低于平均值，因此当您继续`xsl:if`调试过程时，条件应该会成功。

## <a name="step-through-the-code"></a>单步执行代码

1. 按**F5**继续。

   由于第一个图书节点满足`xsl:if`条件，因此图书节点将添加到*低于平均值.xml*输出文件中。 调试器继续执行，直到它再次位于样式表中的 `xsl:if` 元素上。 调试器现在位于*book.xml*文件中的第二个书籍节点上。

   在 **"监视 1"** 窗口中`self::node()`，值将更改为第二个书籍节点。 通过检查 price 元素的值，可以确定价格高于平均值，所以，`xsl:if` 条件应失败。

2. 按**F5**继续。

   由于第二个书籍节点不符合条件`xsl:if`，因此不会将书籍节点添加到*低于平均值.xml*输出文件中。 调试器将继续执行，直到它再次定位在样式表中`xsl:if`的元素上。 调试器现在位于*book.xml*文件中`book`的第三个节点上。

   在 **"监视 1"** 窗口中`self::node()`，值将更改为第三个书籍节点。 通过检查元素的值，`price`可以确定价格低于平均值。 条件`xsl:if`应成功。

3. 按**F5**继续。

   由于`xsl:if`条件得到满足，因此第三本书将添加到*低于平均值.xml*输出文件中。 XML 文档中的所有 book 节点均已处理，调试程序停止。

## <a name="sample-files"></a>示例文件

下列两个文件供该演练使用。

### <a name="below-averagexsl"></a>低于平均水平.

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

## <a name="see-also"></a>另请参阅

- [调试 XSLT](../xml-tools/debugging-xslt.md)
