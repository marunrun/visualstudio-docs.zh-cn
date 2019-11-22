---
title: XML 工具
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
f1_keywords:
- vb.xmldesigner
helpviewer_keywords:
- XML [Visual Studio], resources
- Enterprise Templates, XML and
- discovery files, XML
- server controls, XML and
- Web server controls, XML
- XSL
- XML [Visual Studio], data sources
- XML schemas
- XML [Visual Studio], SGML relationship to
- CSS, style sheets for XML
- XML [Visual Studio], .NET Framework classes
- data [Visual Studio], XML
- classes [Visual Studio], XML
- style sheets, for XML
- Web services
- SGML, XML
- XML [Visual Studio]
- datasets [Visual Basic], XML Schemas
- XSD schemas
- XSL, style sheets
- XMLDataDocument class
ms.assetid: 1fd5de47-2d61-4180-9539-c2c4bf9ab768
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3ee0cf61f8ec2787894c6f67b8ac75424246c507
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297447"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio 中的 XML 工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extensible Markup Language (XML)* is a markup language that provides a format for describing data. 该语言使跨越多个平台进行更准确的内容声明和获得更有意义的搜索结果变得更加容易。 此外，XML 实现了表示与数据的分离。 例如，在 HTML 中，使用标记来告诉浏览器将数据显示为粗体或斜体；而在 XML 中，标记只用于描述数据，例如城市名、温度和大气压。 在 XML 中，使用样式表（例如，可扩展样式表语言 (XSL) 和层叠样式表 (CSS)）在浏览器中显示数据。 XML 将数据与表示及处理相分离。 这一特点使你能够通过应用不同的样式表和应用程序，按照所需的方式显示和处理数据。

 XML 是为在 Web 上传送而优化了的 SGML 的子集。 它是由万维网联合会 (W3C) 定义的。 此标准化确保了结构化数据的统一性和相对于应用程序或供应商的独立性。

 XML 是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 的许多功能的核心。 下面的主题列表列出了 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 中提供的与 XML 相关的工具和功能。

 For more information, see the [XML Developer Center](https://go.microsoft.com/fwlink/?LinkID=100176), which provides the latest documentation, technical information, downloads, newsgroups, and other resources for XML developers.

## <a name="in-this-section"></a>本节内容
 [Working with XML Data](../xml-tools/working-with-xml-data.md) Discusses the role of XML in the way data is handled in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].

 [Debugging XSLT](../xml-tools/debugging-xslt.md) Provides links to topics about using the Visual Studio debugger to debug XSLT.

## <a name="reference"></a>参考
 [Microsoft.VisualStudio.XmlEditor](https://go.microsoft.com/fwlink/?LinkID=165699) Exposes the [XML Editor](https://go.microsoft.com/fwlink/?LinkId=228249) parse tree through [System.Xml.Linq](https://go.microsoft.com/fwlink/?LinkId=228250) for any XML documents.

 [XML Standards Reference](https://msdn.microsoft.com/79c78508-c9d0-423a-a00f-672e855de401) Provides information about XML technologies, including XML, Document Type Definition (DTD), XML Schema definition language (XSD), and XSLT.

 <xref:System.Xml?displayProperty=fullName> Describes the classes and other elements that make up the <xref:System.Xml> namespace and provides links to more detailed information on each item.

 <xref:System.Xml.Serialization?displayProperty=fullName> Describes the classes and other elements that make up the <xref:System.Xml.Serialization> namespace and provides links to more detailed information about each item.

## <a name="related-sections"></a>相关章节
 [XML Document Object Model (DOM)](https://msdn.microsoft.com/library/b5e52844-4820-47c0-a61d-de2da33e9f54) Describes how the <xref:System.Xml.XmlDocument> and its associated classes comply with the W3C Document Object Model (Core) Level 1 and Level 2 namespace support specifications.

 [Reading XML with the XmlReader](https://msdn.microsoft.com/3029834c-a27e-4331-b7aa-711924062182) Describes how the <xref:System.Xml.XmlReader> provides noncached, forward only, read-only access to XML data over an XML stream.

 [Writing XML with the XmlWriter](https://msdn.microsoft.com/ea41f72c-e1d3-4e0a-ab0f-f0eb1c27ab86) Describes how the <xref:System.Xml.XmlWriter> provides noncached, forward only, way of generating XML streams and helps you build XML documents that comply with the W3C standard.

 [XSLT Transformations](https://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03) Describes how the <xref:System.Xml.Xsl.XslCompiledTransform> class implements the XSLT 1.0 recommendation.

 [Process XML Data Using the XPath Data Model](https://msdn.microsoft.com/library/536c6fce-1453-4654-9c72-bca54d47e081) Describes how the <xref:System.Xml.XPath.XPathNavigator> class can process XML data stored in an <xref:System.Xml.XPath.XPathDocument> or an <xref:System.Xml.XmlDocument> object. <xref:System.Xml.XPath.XPathNavigator> 类以 XQuery 1.0 和 XPath 2.0 数据模型为基础，可用于导航和编辑 XML 数据。

 [XML Schema Object Model (SOM)](https://msdn.microsoft.com/library/a897a599-ffd1-43f9-8807-e58c8a7194cd) Describes the classes used for creating and manipulating XML Schemas, by providing an <xref:System.Xml.Schema.XmlSchema> class to load and edit a schema.
