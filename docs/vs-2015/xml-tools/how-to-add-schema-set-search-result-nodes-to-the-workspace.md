---
title: 如何：将架构集搜索结果节点添加到工作区 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: ff33b3cc-4db9-4b4e-9378-b45ed5999b18
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4fc312d4120ef8d1d0f2deb5acd3ce581e878570
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63447122"
---
# <a name="how-to-add-schema-set-search-result-nodes-to-the-workspace"></a>如何：将架构集搜索结果节点添加到工作区
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何将 XML 架构资源管理器中作为关键字搜索结果突出显示的节点添加到工作区中。  
  
> [!NOTE]
> 只能将全局节点可以添加到[工作区](../xml-tools/xml-schema-designer-workspace.md)。  
  
 此示例使用示例[采购订单架构](../xml-tools/sample-xsd-file-purchase-order-schema.md)。  
  
### <a name="to-add-schema-set-result-nodes"></a>添加架构集结果节点  
  
1. 按照中的步骤[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)。  
  
2. 中的搜索文本框中键入"purchaseOrder" [XML 资源管理器](../xml-tools/xml-schema-explorer.md)工具栏，然后单击搜索按钮。  
  
     ![XML 架构资源管理器关键字搜索](../xml-tools/media/schemaexplorersearch.gif "SchemaExplorerSearch")  
  
     搜索结果将突出显示在 XML 架构资源管理器中，并用垂直滚动条上的刻度标记。  
  
3. 单击将搜索结果添加到工作区**突出显示的节点添加到工作区**摘要结果窗格上的按钮。  
  
     ![XML 架构资源管理器搜索结果](../xml-tools/media/schemaexplorersearchresult.gif "SchemaExplorerSearchResult")  
  
     `purchaseOrder`节点和`PurchaseOrderType`节点的设计图面上显示彼此[关系图视图](../xml-tools/graph-view.md)。 因为这两个节点相关（`purchaseOrder` 元素属于 `PurchaseOrderType` 类型），因此会在这两个节点之间绘制一个箭头。
