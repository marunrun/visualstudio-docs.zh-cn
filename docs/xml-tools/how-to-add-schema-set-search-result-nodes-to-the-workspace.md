---
title: 将 XML 架构集搜索结果节点添加到工作区
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ff33b3cc-4db9-4b4e-9378-b45ed5999b18
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1bdb21c2b9ce3f6a79bf24738c84fcb3064c24cb
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592784"
---
# <a name="how-to-add-schema-set-search-result-nodes-to-the-workspace"></a>如何：将架构集搜索结果节点添加到工作区

本主题说明如何将**XML 架构资源管理器**中突出显示的节点作为工作区中关键字搜索的结果添加。

> [!NOTE]
> 只能将全局节点添加到[工作区](../xml-tools/xml-schema-designer-workspace.md)。

此示例使用示例[采购订单架构](../xml-tools/sample-xsd-file-purchase-order-schema.md)。

## <a name="to-add-schema-set-result-nodes"></a>添加架构集结果节点

1. 按照[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)中的步骤操作。

2. 在 " [XML 资源管理器](../xml-tools/xml-schema-explorer.md)" 工具栏的 "搜索" 文本框中键入 "purchaseOrder"，然后单击搜索按钮。

     ![XML 架构资源管理器关键字搜索](../xml-tools/media/schemaexplorersearch.gif)

     搜索结果在**XML 架构资源管理器**中突出显示，并由垂直滚动条上的刻度标记。

3. 单击摘要结果窗格上的 "**将突出显示的节点添加到工作区**" 按钮，将搜索结果添加到工作区。

     ![XML 架构资源管理器搜索结果](../xml-tools/media/schemaexplorersearchresult.gif)

     "`purchaseOrder`" 节点和 "`PurchaseOrderType`" 节点在[图形视图](../xml-tools/graph-view.md)的设计图面上彼此相邻显示。 因为这两个节点相关（`purchaseOrder` 元素属于 `PurchaseOrderType` 类型），因此会在这两个节点之间绘制一个箭头。
