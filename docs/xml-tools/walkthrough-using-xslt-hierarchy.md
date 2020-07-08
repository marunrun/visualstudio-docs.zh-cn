---
title: 演练：使用 XSLT 层次结构
ms.date: 11/04/2016
ms.topic: how-to
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 940185687544b22325d3f75751eb92e950deb685
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815027"
---
# <a name="walkthrough-use-xslt-hierarchy"></a>演练：使用 XSLT 层次结构

XSLT 层次结构工具简化了诸多 XML 开发任务。 XSLT 样式表通常使用 `includes` 和 `imports` 指令。 编译从主体样式表开始，但看到因编译 XSLT 样式表而发生的错误时，该错误可能来自其他源而不是来自主体样式表。 修复该错误或编辑样式表可能需要访问包含的或已导入的样式表。 在调试器中逐项通过样式表，可能会打开已包含和已导入的样式表，并且可能需要在一个或多个已包含样式表中的某个位置添加断点。

当要在内置模板规则上放置断点时，XSLT 层次结构工具也会很有用。 模板规则是针对样式表的各种模式生成的特定模板，当没有其他模板匹配节点时，由 `xsl:apply-templates` 调用。 为完成内置模板规则中的调试，XSLT 调试器使用临时文件夹中的规则生成文件，并将它们与主体样式表一起编译。 如果没有从某些 `xsl:apply-template` 单步执行代码，将很难找到已包含在主体样式表中的样式表，或很难找到和打开带内置模板规则的样式表。

本主题中的示例演示了所引用样式表中的调试。

## <a name="to-debug-in-a-referenced-style-sheet"></a>在引用样式表中进行调试

1. 在 Visual Studio 中打开 XML 文档。 本示例使用下列文档：

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <?xml-stylesheet type="text/xsl" href="xslinclude.xsl"?>
    <COLLECTION>
      <BOOK>
        <TITLE>Lover Birds</TITLE>
        <AUTHOR>Cynthia Randall</AUTHOR>
        <PUBLISHER>Lucerne Publishing</PUBLISHER>
      </BOOK>
      <BOOK>
        <TITLE>The Sundered Grail</TITLE>
        <AUTHOR>Eva Corets</AUTHOR>
        <PUBLISHER>Lucerne Publishing</PUBLISHER>
      </BOOK>
      <BOOK>
        <TITLE>Splish Splash</TITLE>
        <AUTHOR>Paula Thurman</AUTHOR>
        <PUBLISHER>Scootney</PUBLISHER>
      </BOOK>
    </COLLECTION>
    ```

1. 添加以下 xslincludefile.xsl：

    ```xml
    <?xml version='1.0'?>
    <xsl:stylesheet version="1.0"
          xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
          xml:space="preserve">

    <xsl:template match="TITLE">
       Title - <xsl:value-of select="."/><BR/>
    </xsl:template>

    <xsl:template match="AUTHOR">
       Author - <xsl:value-of select="."/><BR/>
    </xsl:template>

    <xsl:template match="PUBLISHER">
       Publisher - <xsl:value-of select="."/><BR/><!-- removed second <BR/> -->
    </xsl:template>

    </xsl:stylesheet>
    ```

3. 添加以下 xslinclude.xsl 文件：

    ```xml
    <?xml version='1.0'?>
    <xsl:stylesheet version="1.0"
          xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

      <xsl:output method="xml" omit-xml-declaration="yes"/>

      <xsl:template match="/">
        <xsl:for-each select="COLLECTION/BOOK">
          <xsl:apply-templates select="TITLE"/>
          <xsl:apply-templates select="AUTHOR"/>
          <xsl:apply-templates select="PUBLISHER"/>
          <BR/>
          <!-- add this -->
        </xsl:for-each>
      </xsl:template>

      <!-- The following template rule will not be called,
      because the related template in the including stylesheet
      is called. If we move this template so that
      it follows the xsl:include instruction, this one
      will be called instead.-->
      <xsl:template match="TITLE">
        <DIV STYLE="color:blue">
          Title: <xsl:value-of select="."/>
        </DIV>
      </xsl:template>

      <xsl:include href="xslincludefile.xsl" />
    </xsl:stylesheet>
    ```

4. 在以下指令位置添加断点：`<xsl:include href="xslincludefile.xsl" />`。

5. 开始调试。

6. 当调试器在指令 `<xsl:include href="xslincludefile.xsl" />` 处停止运行时，请按“单步执行”按钮。 该调试可在所引用的样式表中继续进行。 该层次结构可见，并且设计器显示正确的路径。

## <a name="see-also"></a>请参阅

- [XSLT 探查器](../xml-tools/xslt-profiler.md)
