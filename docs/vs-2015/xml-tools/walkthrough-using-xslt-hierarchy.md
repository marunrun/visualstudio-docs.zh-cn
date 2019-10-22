---
title: 演练：使用 XSLT 层次结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 5e60c8ec-cd05-4597-b856-55038218acf4
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 46e6acc8f65a9c9589348508f57cc75b04c61ccc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669550"
---
# <a name="walkthrough-using-xslt-hierarchy"></a>演练：使用 XSLT 层次结构
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XSLT 层次结构工具简化了诸多 XML 开发任务。 XSLT 样式表通常使用 `includes` 和 `imports` 指令。 编译从主体样式表开始，但看到因编译 XSLT 样式表而发生的错误时，该错误可能来自其他源而不是来自主体样式表。 修复该错误或编辑样式表可能需要访问包含的或已导入的样式表。 在调试器中逐项通过样式表，可能会打开已包含和已导入的样式表，并且可能需要在一个或多个已包含样式表中的某个位置添加断点。

 当要在内置模板规则上放置断点时，XSLT 层次结构工具也会很有用。 模板规则是针对样式表的各种模式生成的特定模板，当没有其他模板匹配节点时，由 `xsl:apply-templates` 调用。 为完成内置模板规则中的调试，XSLT 调试器使用临时文件夹中的规则生成文件，并将它们与主体样式表一起编译。 如果没有从某些 `xsl:apply-template` 单步执行代码，将很难找到已包含在主体样式表中的样式表，或很难找到和打开带内置模板规则的样式表。

 本主题中的示例演示了所引用样式表中的调试。

### <a name="procedure-title"></a>过程标题

1. 在 Visual Studio 中打开 XML 文档。 本示例使用下列 `collection.xml` 文档。

    ```
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

2. 添加以下 `xslincludefile.xsl`：

    ```
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

3. 添加以下 `xslinclude.xsl` 文件：

    ```
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

4. 在以下指令位置添加断点：`<xsl:include href="xslincludefile.xsl" />`

5. 开始调试。

6. 当调试器在指令 `<xsl:include href="xslincludefile.xsl" />` 处停止运行时，请按“逐语句”按钮。 请注意，该调试可在所引用的样式表中继续进行。 该层次结构可见，并且设计器显示正确的路径。

## <a name="see-also"></a>请参阅
 [演练：XSLT 探查器](../xml-tools/walkthrough-xslt-profiler.md)
