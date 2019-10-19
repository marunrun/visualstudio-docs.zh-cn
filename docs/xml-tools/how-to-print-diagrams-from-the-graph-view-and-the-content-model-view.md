---
title: XML 架构：图形视图中的打印关系图 & 内容模型视图
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7e1785e4-4aaf-4c66-8735-51e7ca035565
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c4d25ef33e22055ff6e6aa17797fcd0c4dbcb0e4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668791"
---
# <a name="how-to-print-diagrams-from-the-graph-view-and-the-content-model-view"></a>如何：从图形视图和内容模型视图打印关系图

本主题介绍如何从图形视图或 XML 架构设计器的内容模型视图打印关系图。

## <a name="to-print-diagrams-from-the-xml-schema-designer"></a>从 XML 架构设计器中打印关系图

1. 在 Visual Studio 中打开 XSD 文件，并将一些节点添加到[XML 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)。

2. 通过使用图形视图或内容模型视图的设计图面中的 "将**关系图导出为图像**上下文（右键单击）" 菜单项将关系图导出到 XPS 文件。

     从关系图视图导出关系图时，整个设计图面将导出到 XPS 文件。 当您从内容模型视图导出关系图，并且在内容模型视图的设计图面上出现多个节点时，只会将第一个节点导出到 XPS 文件。

3. 通过使用 XPS 查看器，打印在 XPS 文件中保存的图像。

## <a name="see-also"></a>请参阅

- [图形视图](../xml-tools/graph-view.md)
- [内容模型视图](../xml-tools/content-model-view.md)
- [XML 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)