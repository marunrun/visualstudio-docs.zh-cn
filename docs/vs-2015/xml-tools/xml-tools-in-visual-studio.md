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
ms.openlocfilehash: b9a46523c4c856367e77c345c7e44d0dbc87508f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75845976"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio 中的 XML 工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可扩展标记语言 (XML) * 是一种提供格式来描述数据的标记语言。 该语言使跨越多个平台进行更准确的内容声明和获得更有意义的搜索结果变得更加容易。 此外，XML 实现了表示与数据的分离。 例如，在 HTML 中，使用标记来告诉浏览器将数据显示为粗体或斜体；而在 XML 中，标记只用于描述数据，例如城市名、温度和大气压。 在 XML 中，使用样式表（例如，可扩展样式表语言 (XSL) 和层叠样式表 (CSS)）在浏览器中显示数据。 XML 将数据与表示及处理相分离。 这一特点使你能够通过应用不同的样式表和应用程序，按照所需的方式显示和处理数据。

 XML 是为在 Web 上传送而优化了的 SGML 的子集。 它是由万维网联合会 (W3C) 定义的。 此标准化确保了结构化数据的统一性和相对于应用程序或供应商的独立性。

 XML 是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 的许多功能的核心。 下面的主题列表列出了 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 中提供的与 XML 相关的工具和功能。

 有关详细信息，请参阅 [Xml 开发人员中心](https://msdn.microsoft.com/data/bb190600.aspx)，其中提供了有关 xml 开发人员的最新文档、技术信息、下载、新闻组和其他资源。

## <a name="in-this-section"></a>本节内容
 使用[XML 数据](../xml-tools/working-with-xml-data.md)讨论 XML 在中处理数据的方式的角色 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

 [调试 XSLT](../xml-tools/debugging-xslt.md) 提供相关主题的链接，这些主题介绍如何使用 Visual Studio 调试程序调试 XSLT。

## <a name="reference"></a>参考
 [Microsoft.VisualStudio.Xml编辑器](https://msdn.microsoft.com/library/microsoft.visualstudio.xmleditor.aspx) 通过System.Xml 公开 [XML 编辑器](https://msdn.microsoft.com/library/ms255810.aspx) 分析树 [ 。Linq](https://msdn.microsoft.com/library/system.xml.linq.aspx) for ANY XML 文档。

 [XML 标准参考](https://msdn.microsoft.com/79c78508-c9d0-423a-a00f-672e855de401) 提供有关 XML 技术的信息，包括 XML、文档类型定义 (DTD) 、XML 架构定义语言 (XSD) 和 XSLT。

 <xref:System.Xml?displayProperty=fullName> 介绍组成命名空间的类和其他元素 <xref:System.Xml> ，并提供指向每个项的更详细信息的链接。

 <xref:System.Xml.Serialization?displayProperty=fullName> 介绍组成命名空间的类和其他元素， <xref:System.Xml.Serialization> 并提供指向有关每个项的更多详细信息的链接。

## <a name="related-sections"></a>相关章节
 [XML 文档对象模型 (DOM) ](https://msdn.microsoft.com/library/b5e52844-4820-47c0-a61d-de2da33e9f54) 描述 <xref:System.Xml.XmlDocument> 及其关联类如何符合 W3C 文档对象模型 (核心) 级别1和级别2命名空间支持规范。

 [用 XmlReader 读取 XML](https://msdn.microsoft.com/3029834c-a27e-4331-b7aa-711924062182) 介绍如何对 <xref:System.Xml.XmlReader> xml 流提供对 xml 数据的非缓存、只进、只读访问。

 [用 XmlWriter 编写 XML](https://msdn.microsoft.com/ea41f72c-e1d3-4e0a-ab0f-f0eb1c27ab86) 介绍如何 <xref:System.Xml.XmlWriter> 提供非缓存、只进、生成 xml 流的方法，并帮助您生成符合 W3C 标准的 xml 文档。

 [XSLT 转换](https://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03) 描述类如何 <xref:System.Xml.Xsl.XslCompiledTransform> 实现 XSLT 1.0 建议。

 [使用 XPath 数据模型处理 XML 数据](https://msdn.microsoft.com/library/536c6fce-1453-4654-9c72-bca54d47e081) 描述类如何 <xref:System.Xml.XPath.XPathNavigator> 处理存储在或对象中的 XML 数据 <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> 。 <xref:System.Xml.XPath.XPathNavigator> 类以 XQuery 1.0 和 XPath 2.0 数据模型为基础，可用于导航和编辑 XML 数据。

 [XML 架构对象模型 (SOM) ](https://msdn.microsoft.com/library/a897a599-ffd1-43f9-8807-e58c8a7194cd) 介绍用于创建和操作 XML 架构的类，通过提供用于 <xref:System.Xml.Schema.XmlSchema> 加载和编辑架构的类。
