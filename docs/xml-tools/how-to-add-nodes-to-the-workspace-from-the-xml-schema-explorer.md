---
title: 从 XML 架构资源管理器向工作区添加节点
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3b5a5749-9693-4b29-b0c2-8e07e0e55514
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 22ff9e7ede2861577403eb09d549911afef0f0a5
ms.sourcegitcommit: ba5e072c9fedeff625a1332f22dcf3644d019f51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432186"
---
# <a name="how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer"></a>如何：将 XML 结构资源管理器中的节点添加到工作区

本主题说明如何将节点添加到[XML 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)从**XML 架构资源管理器**。 这可以通过拖放节点从实现**XML 架构资源管理器**到 XSD 设计器视图，或使用**XML 架构资源管理器的**上下文菜单。 您还可以添加作为执行的搜索结果突出显示的节点**XML 架构资源管理器**。 有关详细信息，请参阅[如何：将架构集搜索结果节点添加到工作区](../xml-tools/how-to-add-schema-set-search-result-nodes-to-the-workspace.md)。

> [!NOTE]
> 只能将全局节点可以添加到[XML 架构设计器工作区](../xml-tools/xml-schema-designer-workspace.md)。

## <a name="to-add-nodes-through-the-xml-explorer-context-menu"></a>若要添加节点通过 XML 资源管理器上下文菜单

1. 按照中的步骤[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)。

2. 右键单击`PurchaseOrderType`XSD 资源管理器中的节点。 选择**关系图视图中显示**。

     `purchaseOrderType` 节点出现在图形视图的设计图面上。

## <a name="to-drag-and-drop-a-node-on-to-a-view"></a>将节点拖放到视图

1. 右键单击`PurchaseOrderType`关系图视图中的节点。 选择**在 XML 架构资源管理器中显示**。

     节点在突出显示**XML 架构资源管理器**。

2. 右键单击`PurchaseOrderType`中的节点**XML 架构资源管理器**，然后选择**显示所有引用**。

     `purchaseOrder` 节点将突出显示。

3. 将 `purchaseOrder` 节点拖到图形视图上。

     `purchaseOrder` 节点和 `PurchaseOrderType` 节点在图形视图的设计图面上紧挨着出现。 因为这两个节点相关（`purchaseOrder` 元素属于 `PurchaseOrderType` 类型），因此会在这两个节点之间绘制一个箭头。

## <a name="to-add-nodes-using-the-schema-explorer-search-capability"></a>使用架构资源管理器的搜索功能添加节点

1. 中的搜索文本框中键入"purchaseOrder" [XML 资源管理器](../xml-tools/xml-schema-explorer.md)工具栏，然后单击搜索按钮。

     ![XML 架构资源管理器关键字搜索](../xml-tools/media/schemaexplorersearch.gif)

     搜索结果中突出显示**XML 架构资源管理器**和按垂直滚动条上的刻度标记。

2. 单击将搜索结果添加到工作区**突出显示的节点添加到工作区**摘要结果窗格上的按钮。

     ![XML 架构资源管理器搜索结果](../xml-tools/media/schemaexplorersearchresult.gif)

     `purchaseOrder`节点和`PurchaseOrderType`节点的设计图面上显示彼此[关系图视图](../xml-tools/graph-view.md)。 因为这两个节点相关（`purchaseOrder` 元素属于 `PurchaseOrderType` 类型），因此会在这两个节点之间绘制一个箭头。

## <a name="see-also"></a>请参阅

- [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)