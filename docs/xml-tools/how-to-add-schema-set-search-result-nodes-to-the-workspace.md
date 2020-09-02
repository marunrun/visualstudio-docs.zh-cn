---
title: 向工作区添加 XML 架构集搜索结果节点
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ff33b3cc-4db9-4b4e-9378-b45ed5999b18
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d94544fd017809b32b7a144b16da4515e6b2e4bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85816314"
---
# <a name="how-to-add-schema-set-search-result-nodes-to-the-workspace"></a>如何：向工作区添加架构集搜索结果节点

本主题介绍如何将 XML 架构资源管理器中作为关键字搜索结果突出显示的节点添加到工作区中。

> [!NOTE]
> 只能将全局节点添加到[工作区](../xml-tools/xml-schema-designer-workspace.md)中。

本示例使用[订单架构](../xml-tools/sample-xsd-file-purchase-order-schema.md)示例。

## <a name="to-add-schema-set-result-nodes"></a>添加架构集结果节点

1. 按照[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)中的步骤操作。

2. 在 [XML 资源管理器](../xml-tools/xml-schema-explorer.md)工具栏的搜索文本框中键入“purchaseOrder”，然后单击搜索按钮。

     ![XML 架构资源管理器关键字搜索](../xml-tools/media/schemaexplorersearch.gif)

     搜索结果将突出显示在 XML 架构资源管理器中，并用垂直滚动条上的刻度标记。

3. 通过在摘要结果窗格中单击“将突出显示的节点添加到工作区”按钮，向工作区添加搜索结果。

     ![XML 架构资源管理器搜索结果](../xml-tools/media/schemaexplorersearchresult.gif)

     `purchaseOrder` 节点和 `PurchaseOrderType` 节点在[图形视图](../xml-tools/graph-view.md)的设计图面上紧挨着出现。 因为这两个节点相关（`purchaseOrder` 元素属于 `PurchaseOrderType` 类型），因此会在这两个节点之间绘制一个箭头。
