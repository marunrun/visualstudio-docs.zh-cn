---
title: XML 架构设计器：使用图形视图获取架构集概述
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c0df4b0d-52ef-4a6c-9676-1d8311aad7c7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f066bc96cd5acf314150def2e40ec3064d154b8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592667"
---
# <a name="how-to-get-an-overview-of-a-schema-set-using-the-graph-view"></a>如何：使用图形视图获取架构集的概述

本主题介绍如何使用[图形视图](../xml-tools/graph-view.md)来查看架构集中节点的高级视图以及节点之间的关系。

## <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>创建新的 XSD 文件并显示内容模型视图中的根元素

1. 创建一个新的 XML 架构文件并将该文件另存为 "*关系"。*

2. 单击 "使用 XML 编辑器" 可以在 "开始" 视图中**查看和编辑基础 XML 架构文件**链接。

3. 从[示例 xml 架构：关系](../xml-tools/sample-xsd-file-relationships.md)中复制 XML 架构示例代码，并将其粘贴以替换默认情况下添加到新 XSD 文件中的代码。

4. 右键单击 XML 编辑器中的任意位置，然后选择 "**视图设计器**"。

5. 从**XSD 工具栏**中选择图形视图。

6. 在**XML 架构资源管理器**中选择 "**架构集**" 节点，然后将该节点拖到图形视图的设计图面中。 您应当会看到所有全局节点，以及连接有关系节点的箭头。

     ![图形视图](../xml-tools/media/relationshipingraphview.gif)

7. 单击设计图面上的任何节点并查看痕迹栏，以了解所选节点在架构集中的位置。

8. Rick-单击设计图面上的任意元素节点，然后选择 "**生成示例 xml** "，查看 XML 实例文档。
