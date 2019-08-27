---
title: 如何：获取架构集使用图形视图的概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: c0df4b0d-52ef-4a6c-9676-1d8311aad7c7
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f6f264427e10cbe444cab8a5208e86866635ed17
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150727"
---
# <a name="how-to-get-an-overview-of-a-schema-set-using-the-graph-view"></a>如何：使用图形视图获取架构集的概览
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何使用[关系图视图](../xml-tools/graph-view.md)若要查看的节点在架构集中，并在节点之间的关系的高级视图。  
  
### <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>创建新的 XSD 文件并显示内容模型视图中的根元素  
  
1. 创建新的 XML 架构文件并将文件保存为 Relationships.xsd。  
  
2. 单击**使用 XML 编辑器查看和编辑基础 XML 架构文件**起始视图上的链接。  
  
3. 中的 XML 架构示例代码复制[示例 XML 架构：关系](../xml-tools/sample-xsd-file-relationships.md)并粘贴以替换默认情况下，已将它们添加到新 XSD 文件的代码。  
  
4. 在 XML 编辑器中的任意位置单击鼠标右键，然后选择**视图设计器**。  
  
5. 从 XSD 工具栏选择图形视图。  
  
6. 选择**架构集**图形视图的设计图面上的 XML 架构资源管理器和拖动节点中的节点。 您应当会看到所有全局节点，以及连接有关系节点的箭头。  
  
     ![图形视图](../xml-tools/media/relationshipingraphview.gif "RelationshipInGraphView")  
  
7. 单击设计图面上的任何节点并查看痕迹栏，以了解所选节点在架构集中的位置。  
  
8. 在设计图面，然后选择任何元素节点上右击**生成示例 XML**若要查看 XML 实例文档。
