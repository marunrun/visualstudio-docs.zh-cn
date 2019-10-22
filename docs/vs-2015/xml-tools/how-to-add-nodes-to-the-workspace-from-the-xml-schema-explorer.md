---
title: 如何：从 XML 架构资源管理器将节点添加到工作区 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 3b5a5749-9693-4b29-b0c2-8e07e0e55514
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e0c8fe9d5ba8c096a03de7a9df85945f4aeb4a0a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656345"
---
# <a name="how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer"></a>如何：从 XML 架构资源管理器向工作区添加节点
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题说明如何从 XML 架构资源管理器将节点添加到[Xml 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)。 这可以通过将节点从 XML 架构资源管理器拖放到 XSD 设计器视图，或使用 XML 架构资源管理器的上下文菜单来实现。 还可以添加由于 XML 架构资源管理器执行的搜索而突出显示的节点。 有关详细信息，请参阅[如何：将架构集搜索结果节点添加到工作区](../xml-tools/how-to-add-schema-set-search-result-nodes-to-the-workspace.md)。

> [!NOTE]
> 只能将全局节点添加到[XML 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)。

### <a name="to-add-nodes-through-the-xml-explorer-context-menu"></a>通过 XML 资源管理器上下文菜单添加节点

1. 按照[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)中的步骤操作。

2. 在 XSD 资源管理器中右击 `PurchaseOrderType` 节点。 选择 **"在关系图视图中显示"** 。

     `purchaseOrderType` 节点出现在图形视图的设计图面上。

### <a name="to-drag-and-drop-a-node-on-to-a-view"></a>将节点拖放到视图

1. 在图形视图中右击 `PurchaseOrderType` 节点。 选择 **"在 XML 架构资源管理器中显示"** 。

     该节点在 XML 架构资源管理器中突出显示。

2. 在 XML 架构资源管理器中右键单击 "`PurchaseOrderType`" 节点，然后选择 "**显示所有引用**"。

     `purchaseOrder` 节点将突出显示。

3. 将 `purchaseOrder` 节点拖到图形视图上。

     `purchaseOrder` 节点和 `PurchaseOrderType` 节点在图形视图的设计图面上紧挨着出现。 因为这两个节点相关（`purchaseOrder` 元素属于 `PurchaseOrderType` 类型），因此会在这两个节点之间绘制一个箭头。

### <a name="to-add-nodes-using-the-schema-explorer-search-capability"></a>使用架构资源管理器的搜索功能添加节点

1. 在 " [XML 资源管理器](../xml-tools/xml-schema-explorer.md)" 工具栏的 "搜索" 文本框中键入 "purchaseOrder"，然后单击搜索按钮。

     ![XML 架构资源管理器关键字搜索](../xml-tools/media/schemaexplorersearch.gif "SchemaExplorerSearch")

     搜索结果将突出显示在 XML 架构资源管理器中，并用垂直滚动条上的刻度标记。

2. 单击摘要结果窗格上的 "**将突出显示的节点添加到工作区**" 按钮，将搜索结果添加到工作区。

     ![XML 架构资源管理器搜索结果](../xml-tools/media/schemaexplorersearchresult.gif "SchemaExplorerSearchResult")

     "@No__t_0" 节点和 "`PurchaseOrderType`" 节点在[图形视图](../xml-tools/graph-view.md)的设计图面上彼此相邻显示。 因为这两个节点相关（`purchaseOrder` 元素属于 `PurchaseOrderType` 类型），因此会在这两个节点之间绘制一个箭头。

## <a name="see-also"></a>请参阅
 [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)
