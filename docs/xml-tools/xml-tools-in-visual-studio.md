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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c9412d89ee7d9ad1412f0eaf9fe9341e336a65e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668712"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio 中的 XML 工具

*可扩展标记语言（XML）* 是一种提供格式来描述数据的标记语言。 XML 使用关联的样式表（如可扩展样式表语言（XSL）和级联样式表（CSS））将数据和其演示分离。 Visual Studio 提供了一些工具和功能，可以更加容易地使用 XML、XSLT 和 XML 架构。

## <a name="xml-editor"></a>XML 编辑器

" [Xml 编辑器](xml-editor.md)" 用于编辑 xml 文档。 它提供完整的 XML 语法检查、键入时架构验证、颜色编码和 IntelliSense。 如果提供了架构或文档类型定义，IntelliSense 将使用该架构或文档类型定义列出允许的元素和属性。

其他功能包括：

- XML 代码段支持，包括架构生成的代码段

- 文档大纲显示可展开和折叠元素

- 执行 XSLT 转换并以文本、XML 或 HTML 格式查看结果的功能

- 从 XML 实例文档生成 XML 架构定义语言（XSD）架构的功能

- 支持编辑 XSLT 样式表，包括 IntelliSense 支持

- XML 架构资源管理器

## <a name="xml-schema-designer"></a>XML 架构设计器

[Xml 架构设计器](xml-schema-designer.md)与 Visual STUDIO 和 xml 编辑器集成，使您能够使用 xml 架构定义语言（XSD）架构。

## <a name="xslt-debugging"></a>XSLT 调试

Visual Studio 支持[调试 XSLT 样式表](../xml-tools/debugging-xslt.md)。 使用调试程序，可以在 XSLT 样式表中设置断点，从代码进入并逐行执行 XSLT 样式表，等等。

> [!NOTE]
> XSLT 调试程序仅适用于 Visual Studio Enterprise edition。

## <a name="see-also"></a>请参阅

- <xref:System.Xml?displayProperty=fullName>
- [XSLT 转换](/dotnet/standard/data/xml/xslt-transformations)
- [使用 XPath 数据模型处理 XML 数据](/dotnet/standard/data/xml/process-xml-data-using-the-xpath-data-model)
- [XML 文档对象模型 (DOM)](/dotnet/standard/data/xml/xml-document-object-model-dom)
- [XML 架构对象模型 (SOM)](/dotnet/standard/data/xml/xml-schema-object-model-som)