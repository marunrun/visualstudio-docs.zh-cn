---
title: 如何：使用内容模型视图检查节点的内容模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: c42ddac8-b0e3-48d6-9832-112a19d6c104
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ddadcb0fbd772a5638bf6023b8cf6c18fbd270d7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670856"
---
# <a name="how-to-examine-the-content-model-of-nodes-using-the-content-model-view"></a>如何：使用内容模型视图检查节点的内容模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何使用[内容模型视图](../xml-tools/content-model-view.md)浏览节点。

### <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>创建新的 XSD 文件并显示内容模型视图中的根元素

1. 创建新的 XML 架构文件。

2. 单击 "使用 XML 编辑器"，在 "开始" 视图中**查看和编辑基础 XML 架构文件**。

3. 从[示例 Xml 架构：采购订单架构](../xml-tools/sample-xsd-file-purchase-order-schema.md)中复制 XML 架构示例代码，并将其粘贴以替换默认情况下添加到新 XSD 文件中的代码。

4. 右键单击 "XML 编辑器" 中的 `purchaseOrder` 元素，然后选择 "**在 Xml 资源管理器中显示**"，在 "架构资源管理器" 中选择 `purchaseOrder` 元素。

5. 右键单击 XML 资源管理器中的 `purchaseOrder`，然后选择 "**在内容模型视图中显示**"。

     内容模型视图显示设计图面上的 `purchaseOrder` 元素。

6. 通过双击每个节点或单击每个节点右侧的双箭头，展开 `shipTo`、`billTo` 和 `items` 节点。

     现在 `purchaseOrder` 元素的节点已展开，您可以查看元素的内容模型。

7. 单击 `purchaseOrder` 元素下的任何节点并查看痕迹栏，以了解所选节点在架构集中的位置。

8. 单击 XSD 工具栏中的 "**显示文档**" 按钮可切换文档。 还可以右击设计图面来切换文档。

9. Rick-单击 "`purchaseOrder`" 节点，然后选择 "**生成示例 xml** "，查看 XML 实例文档。
