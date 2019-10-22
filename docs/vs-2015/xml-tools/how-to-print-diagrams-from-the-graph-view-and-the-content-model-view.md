---
title: 如何：从图形视图和内容模型视图打印关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 7e1785e4-4aaf-4c66-8735-51e7ca035565
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: de59aac6bc40e58b6da9b71fd0cc81d432fe41bd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670846"
---
# <a name="how-to-print-diagrams-from-the-graph-view-and-the-content-model-view"></a>如何：从图形视图和内容模型视图打印关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题描述如何从图形视图或内容模型视图中打印关系图。

### <a name="to-print-diagrams-from-the-xml-schema-designer"></a>从 XML 架构设计器中打印关系图

1. 在 Visual Studio 中打开 XSD 文件，并将一些节点添加到[XML 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)。

2. 使用 "将**关系图导出为图像 ...** " 将关系图导出到 XPS 文件。 图形视图或内容模型视图的设计图面中的上下文菜单项。

     当您从图形视图导出关系图时，整个设计图面将被导出到 XPS 文件。 当您从内容模型视图导出关系图，并且多个节点显示在内容模型视图的设计图面上时，只有第一节点会导出到 XPS 文件。

3. 通过使用 XPS 查看器，打印在 XPS 文件中保存的图像。

## <a name="see-also"></a>请参阅
 [图形视图](../xml-tools/graph-view.md)[内容模型视图](../xml-tools/content-model-view.md) [XML 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)
