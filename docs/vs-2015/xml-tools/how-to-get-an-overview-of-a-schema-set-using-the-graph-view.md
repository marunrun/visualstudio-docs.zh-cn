---
title: 如何：使用图形视图获取架构集的概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: c0df4b0d-52ef-4a6c-9676-1d8311aad7c7
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7009e5772b4f4c6977d58d2c52d733999a0d9369
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670895"
---
# <a name="how-to-get-an-overview-of-a-schema-set-using-the-graph-view"></a>如何：使用图形视图获取架构集的概览
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何使用[图形视图](../xml-tools/graph-view.md)来查看架构集中节点的简要视图以及节点间的关系。

### <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>创建新的 XSD 文件并显示内容模型视图中的根元素

1. 创建新的 XML 架构文件并将文件保存为 Relationships.xsd。

2. 单击 "使用 XML 编辑器" 可以在 "开始" 视图中 **查看和编辑基础 XML 架构文件** 链接。

3. 从 [示例 Xml 架构：关系](../xml-tools/sample-xsd-file-relationships.md) 中复制 XML 架构示例代码，并将其粘贴以替换默认情况下添加到新 XSD 文件中的代码。

4. 右键单击 XML 编辑器中的任意位置，然后选择 " **视图设计器**"。

5. 从 XSD 工具栏选择图形视图。

6. 在 XML 架构资源管理器中选择 " **架构集** " 节点，然后将该节点拖到 "图形" 视图的 "设计 suface"。 您应当会看到所有全局节点，以及连接有关系节点的箭头。

     ![图形视图](../xml-tools/media/relationshipingraphview.gif "RelationshipInGraphView")

7. 单击设计图面上的任何节点并查看痕迹栏，以了解所选节点在架构集中的位置。

8. Rick-单击 desing 图面上的任意元素节点，然后选择 " **生成示例 xml** "，查看 XML 实例文档。
