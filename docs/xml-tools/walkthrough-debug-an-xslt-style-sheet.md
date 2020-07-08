---
title: 调试 XSLT 样式表
ms.date: 03/05/2019
ms.topic: how-to
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8c75d3cae07101363f6c986a1defb375f602f466
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815118"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>演练：调试 XSLT 样式表

此演练中的步骤演示如何使用 XSLT 调试程序。 步骤包括查看变量、设置断点和逐行执行代码。 调试器使你可以一次执行一行代码。

若要为此演练做好准备，请先将两个[示例文件](#sample-files)复制到本地计算机上。 一个文件是样式表，另一个是将用作样式表的输入的 XML 文件。 在此演练中，我们使用的样式表会查找成本低于平均书价的所有书籍。

> [!NOTE]
> XSLT 调试器仅适用于 Visual Studio 企业版。

## <a name="start-debugging"></a>“启动调试”

1. 在“文件”菜单中，选择“打开” > “文件”。

2. 找到 below-average.xsl 文件，然后选择“打开”。

   样式表会在 XML 编辑器中打开。

3. 在文档属性窗口的“输入”字段上单击“浏览”按钮 (...)。 （如果“属性”窗口不可见，请在编辑器中打开的文件上右键单击任意位置，然后选择“属性”。）

4. 找到 books.xml 文件，然后选择“打开”。

   这会设置用于 XSLT 转换的源文档文件。

5. 在 below-average.xsl 的第 12 行上设置[断点](../debugger/using-breakpoints.md)。 可以通过多种方法执行此操作：

   - 在第 12 行上的编辑器边距中单击。

   - 单击第 12 行上的任意位置，然后按 F9。

   - 右键单击 `xsl:if` 开始标记，然后选择“端点” > “插入断点”。

      ![在 Visual Studio 中的 XSL 文件中插入断点](media/insert-breakpoint.PNG)

6. 在菜单栏上，选择“XML” > “开始调试 XSLT”（或按 Alt+F5）。

   调试过程随即开始。

   在编辑器中，调试器位于样式表的 `xsl:if` 元素上。 名为 below-average.xml 的另一个文件会在编辑器中打开；这是将在处理输入文件 books.xml 中的每个节点时填充的输出文件。

   “自动”、“局部变量”和“监视 1”窗口会出现在 Visual Studio 窗口底部。 “局部变量”窗口显示所有局部变量及其当前值。 其中包括样式表中定义的变量，也包括调试程序在跟踪上下文中的当前节点时使用的变量。

## <a name="watch-window"></a>监视窗口

我们会将两个变量添加到“监视 1”窗口，以便可以在处理输入文件时检查其值。 （如果要监视的变量已经存在，则还可以使用“局部变量”窗口检查值。）

1. 在“调试”菜单中，选择“窗口” > “监视” > “监视 1”。

   “监视 1”窗口会成为可见状态。

2. 在“名称”字段中键入 `$bookAverage`，然后按 Enter。

   `$bookAverage` 变量的值会显示在“值”窗口中。

3. 在下一行中，在“名称”字段中键入 `self::node()`，然后按 Enter。

   `self::node()` 是一个计算结果为当前上下文节点的 XPath 表达式。 `self::node()` XPath 表达式的值是第一个 book 节点。 此值随着转换的进度而更改。

4. 展开 `self::node()` 节点，然后展开值为 `price` 的节点。

   ![在 Visual Studio 中进行 XSLT 调试时的“监视”窗口](media/xslt-debugging-watch-window.png)

   可以查看当前 book 节点的书价值并将它与 `$bookAverage` 值进行比较。 因为书价低于平均值，所以在继续调试过程时，`xsl:if` 条件应成功。

## <a name="step-through-the-code"></a>逐行执行代码

1. 按 F5 继续。

   因为第一个 book 节点满足 `xsl:if` 条件，所以，该 book 节点将添加到 below-average.xml 输出文件。 调试器继续执行，直到它再次位于样式表中的 `xsl:if` 元素上。 调试器此时位于 books.xml 文件中的第二个 book 节点上。

   在“监视 1”窗口中，`self::node()` 值变为第二个 book 节点。 通过检查 price 元素的值，可以确定价格高于平均值，所以，`xsl:if` 条件应失败。

2. 按 F5 继续。

   因为第二个 book 节点未满足 `xsl:if` 条件，所以不会将此 book 节点添加到 below-average.xml 输出文件。 调试器继续执行，直到它再次位于样式表中的 `xsl:if` 元素上。 调试器此时位于 books.xml 文件中的第三个 `book` 节点上。

   在“监视 1”窗口中，`self::node()` 值变为第三个 book 节点。 通过检查 `price` 元素的值，可以确定此价格低于平均价格。 `xsl:if` 条件应成功。

3. 按 F5 继续。

   因为满足 `xsl:if` 条件，所以，第三个 book 节点将添加到 below-average.xml 输出文件。 XML 文档中的所有 book 节点均已处理，调试程序停止。

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
