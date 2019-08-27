---
title: XML 编辑器和架构设计器
ms.date: 11/04/2016
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
- XML [Visual Studio], .NET classes
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d7493d6c10c83b16ad7579299a49a7747e34c20b
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746518"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio 中的 XML 工具

*可扩展标记语言 (XML)* 是一种标记语言，用于描述数据提供一种格式。 XML 将数据分割开来，并使用其表示关联的样式表等可扩展样式表语言 (XSL) 和级联样式表 (CSS)。 Visual Studio 提供了一些工具和功能，可以更加容易地使用 XML、XSLT 和 XML 架构。

## <a name="xml-editor"></a>XML 编辑器

[XML 编辑器](xml-editor.md)用于编辑 XML 文档。 它提供了完整 XML 语法检查、 键入时，颜色编码和 IntelliSense 时的架构验证。 如果提供了架构或文档类型定义，IntelliSense 将使用该架构或文档类型定义列出允许的元素和属性。

其他功能包括：

- XML 代码段支持，包括架构生成的代码段

- 文档大纲，以便可以展开和折叠元素

- 能够执行 XSLT 转换并以文本、 XML 或 HTML 的形式查看结果

- 从 XML 实例文档生成 XML 架构定义语言 (XSD) 架构的功能

- 支持编辑 XSLT 样式表，包括 IntelliSense 支持

- XML 架构资源管理器

## <a name="xml-schema-designer"></a>XML 架构设计器

[XML 架构设计器](xml-schema-designer.md)集成使用 Visual Studio 和 XML 编辑器，以使你能够使用 XML 架构定义语言 (XSD) 架构。

## <a name="xslt-debugging"></a>XSLT 调试

Visual Studio 支持[调试 XSLT 样式表](../xml-tools/debugging-xslt.md)。 使用调试程序，可以在 XSLT 样式表中设置断点，从代码进入并逐行执行 XSLT 样式表，等等。

> [!NOTE]
> XSLT 调试程序是仅在 Visual Studio Enterprise edition 中可用。

## <a name="see-also"></a>请参阅

- <xref:System.Xml?displayProperty=fullName>
- [XSLT 转换](/dotnet/standard/data/xml/xslt-transformations)
- [使用 XPath 数据模型处理 XML 数据](/dotnet/standard/data/xml/process-xml-data-using-the-xpath-data-model)
- [XML 文档对象模型 (DOM)](/dotnet/standard/data/xml/xml-document-object-model-dom)
- [XML 架构对象模型 (SOM)](/dotnet/standard/data/xml/xml-schema-object-model-som)