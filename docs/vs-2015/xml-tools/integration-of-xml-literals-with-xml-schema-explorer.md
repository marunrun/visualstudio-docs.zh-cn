---
title: XML 文本与 XML 架构资源管理器的集成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 57a29998-c6e8-48ac-bdb0-5788e73f9164
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a15767454c83604de2844e4c0a9f2e121a9a1a4f
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846126"
---
# <a name="integration-of-xml-literals-with-xml-schema-explorer"></a>XML 文本与 XML 架构资源管理器的集成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Basic 支持 XML 文本，这意味着您可以将 XML 片段直接合并到您的 Visual Basic 代码中。 有关详细信息，请参阅[XML 文本概述](https://msdn.microsoft.com/library/bb384629.aspx)。

 如果 Visual Basic 项目中的 XSD 文件包括一个 XML 文本，则可以在 XML 架构资源管理器中查看 XML 架构集。 若要查看与 XML 文本关联的架构集，请右键单击 XML 文本或 XML 命名空间导入中的 XML 节点，然后选择 "**在架构资源管理器中显示**"。

 ![Visual Basic XML 文本;XML 架构资源管理器](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer1.gif "VBXMLLiteralsWithXMLSchemaExplorer1")

 此操作将并行打开 XML 架构资源管理器和 Visual Basic 文件。

 ![Visual Basic XML 文本;XML 架构资源管理器](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer2.gif "VBXMLLiteralsWithXMLSchemaExplorer2")

 Visual Studio 2008 SP1 中已经引入了此功能。 若要观看此功能的详细说明，请参阅第[9 频道： Visual Studio 2008 SP1 中的 XML 架构资源管理器](https://channel9.msdn.com/Blogs/funkyonex/XML-Schema-Explorer-in-Visual-Studio-2008-SP1)。

## <a name="see-also"></a>请参阅
 [如何：将 XML 架构设计器用于 XML 文本](../xml-tools/how-to-use-the-xml-schema-designer-with-xml-literals.md)
