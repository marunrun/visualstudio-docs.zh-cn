---
title: 演练：使用 XSLT IntelliSense
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 079d95ac-2eaf-4ae1-9cd3-2c81a961a942
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a085627d598bfcc969c2e76d717a2f49a31922b2
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817276"
---
# <a name="walkthrough-using-xslt-intellisense"></a>演练：使用 XSLT IntelliSense

此演练演示如何使用 XSLT IntelliSense 自动完成某些特性的值。

## <a name="to-use-intellisense-in-the-name-attribute-of-xslwith-param-and-xslcall-template-elements"></a>在 xsl:with-param 和 xsl:call-template 元素的名称特性中使用 IntelliSense

1. 用下面的代码创建新的 XSLT 文件和副本：

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
    <!-- These 2 elements effectively assign
         $messages = resources/en.xml/<messages>,
         then $messages is used in the "localized-message" template.  -->
    <xsl:param name="lang">en</xsl:param>
    <xsl:variable name="messages"
          select="document(concat('resources/', $lang, '.xml'))/messages"/>

    <xsl:template name="msg23" match="msg23">
    </xsl:template>

    <xsl:template name="localized-message">
      <xsl:param name="msgcode"/>
      <!-- Show message string. -->
      <xsl:message terminate="yes">
        <xsl:value-of select="$messages/message[@name=$msgcode]"/>
      </xsl:message>
    </xsl:template>
    </xsl:stylesheet>
    ```

2. 在 `<xsl:template name="msg23" match="msg23">` 之后插入光标并按 Enter。 然后开始键入以下 `xsl:call-template` 元素：

    ```xml
    <xsl:call-template name="localized-message">
    </xsl:call-template>
    ```

     在键入元素时，模板名称列表出现在 `name=""` 元素的 `xsl:call-template` 特性中。

3. 在 `<xsl:call-template name="localized-message">` 之后插入光标并按 Enter。 然后开始键入以下 `xsl:with-param` 元素：

    ```xml
    <xsl:with-param name="msgcode">msg23</xsl:with-param>
    ```

     参数名称的列表出现在 `name=""` 元素的 `xsl:with-param` 特性中。

## <a name="to-use-intellisense-in-the-mode-attribute-of-an-xslapply-templates-element"></a>在 xsl:apply-templates 元素的模式特性中使用 IntelliSense

1. 用下面的代码创建新的 XSLT 文件和副本：

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
      <xsl:template match="/">
        <HTML>
          <BODY>
            <TABLE>
              <xsl:apply-templates select="customers/customer">
                <xsl:sort select="state"/>
                <xsl:sort select="name"/>
              </xsl:apply-templates>
            </TABLE>
          </BODY>
        </HTML>
      </xsl:template>
      <xsl:template match="customer">
        <TR>
          <xsl:apply-templates select="name" />
          <xsl:apply-templates select="address" />
          <xsl:apply-templates select="phone" />
        </TR>
      </xsl:template>
      <xsl:template match="name">
        <TD STYLE="font-size:14pt font-family:serif">
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="address">
        <TD>
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="phone">
        <TD>
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="phone" mode="accountNumber">
        <xsl:param name="Area_Code"/>
        <TD STYLE="font-style:italic">
          1-<xsl:value-of select="."/>-001
        </TD>
      </xsl:template>
    </xsl:stylesheet>
    ```

2. 在 `<xsl:apply-templates select="phone" />` 之后插入光标并按 Enter。 然后开始键入以下 `xsl: apply-templates` 元素：

    ```xml
    <xsl:apply-templates select="phone"  mode="accountNumber">
    ```

     模板模式的列表出现在 `mode=""` 元素的 `xsl:apply-templates` 特性中。

## <a name="to-use-intellisense-in-the-stylesheet-prefix-and-result-prefix-attributes-of-an-xslnamespace-alias-element"></a>在 xsl:namespace-alias 元素的 stylesheet-prefix 和 result-prefix 特性中使用 IntelliSense

1. 用下面的代码创建新的 XSLT 文件和副本：

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:alt="http://www.w3.org/1999/XSL/Transform-alternate"
    version="1.0">
      <xsl:param name="browser" select="'InternetExplorer'"/>
      <xsl:template match="/">
        <alt:stylesheet>
          <xsl:choose>
            <xsl:when test="$browser='InternetExplorer'">
              <alt:import href="IERoutines.xsl"/>
              <alt:template match="/">
                <div>
                  <alt:call-template name="showTable"/>
                </div>
              </alt:template>
            </xsl:when>
            <xsl:otherwise>
              <alt:import href="OtherBrowserRoutines.xsl"/>
              <alt:template match="/">
                <div>
                  <alt:call-template name="showTable"/>
                </div>
              </alt:template>
            </xsl:otherwise>
          </xsl:choose>
        </alt:stylesheet>
      </xsl:template>
    </xsl:stylesheet>
    ```

2. 在 `<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:alt="http://www.w3.org/1999/XSL/Transform-alternate" version="1.0">` 之后插入光标并按 Enter。 然后开始键入以下 `xsl:namespace-alias` 元素：

    ```xml
    <xsl:namespace-alias stylesheet-prefix="alt" result-prefix="xsl"/>
    ```

     请注意前缀列表在 `stylesheet-prefix` 元素的 `result-prefix` 和 `xsl:namespace-alias` 特性中的显示方式。

## <a name="see-also"></a>请参阅

- [XML 编辑器 IntelliSense 功能](../xml-tools/xml-editor-intellisense-features.md)
