---
title: Integration of XML Literals with XML Schema Explorer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 57a29998-c6e8-48ac-bdb0-5788e73f9164
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d808fce2783d444071ea1a7976d26e3c5bf02eed
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297462"
---
# <a name="integration-of-xml-literals-with-xml-schema-explorer"></a>XML 文本与 XML 架构资源管理器的集成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Basic supports XML literals, which means that you can incorporate XML fragments directly into your Visual Basic code. For more information, see [XML Literals Overview](https://go.microsoft.com/fwlink/?LinkId=140325).

 如果 Visual Basic 项目中的 XSD 文件包括一个 XML 文本，则可以在 XML 架构资源管理器中查看 XML 架构集。 To view the schema set associated with an XML literal, right-click on an XML node in an XML literal or an XML namespace import and select **Show in Schema Explorer**.

 ![Visual Basic XML Literals; XML Schema Explorer](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer1.gif "VBXMLLiteralsWithXMLSchemaExplorer1")

 此操作将并行打开 XML 架构资源管理器和 Visual Basic 文件。

 ![Visual Basic XML Literals; XML Schema Explorer](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer2.gif "VBXMLLiteralsWithXMLSchemaExplorer2")

 Visual Studio 2008 SP1 中已经引入了此功能。 To watch an interview in which this feature is explained in detail, see [Channel 9 Interview : XML Schema Explorer in Visual Studio 2008 SP1](https://channel9.msdn.com/Blogs/funkyonex/XML-Schema-Explorer-in-Visual-Studio-2008-SP1).

## <a name="see-also"></a>请参阅
 [如何：将 XML 架构设计器用于 XML 文本](../xml-tools/how-to-use-the-xml-schema-designer-with-xml-literals.md)
