---
title: XML 架构设计器工作区
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 588fa495-fe7f-4b16-8a9f-6b6b8d2d502a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4cf86dd39e010424b25916deec8cdebd23ee1c1b
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592368"
---
# <a name="xml-schema-designer-workspace-views"></a>XML 架构设计器工作区概述

XML 架构设计器（XSD 设计器）是一个图形工具，可帮助您浏览 XML 架构。 除了 [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)（利用它可以浏览和导航 XML 架构树以及执行搜索）之外，XSD 设计器还提供了三个视图，可以在其中浏览 XSD 架构的更多详细信息。

- 起始视图是 XSD 设计器的启动点；从起始视图可以导航到 XSD 设计器的其他视图，并查看架构集的详细信息。
- 通过图形视图可查看架构集的概览以及架构节点之间的关系。
- 内容模型视图以图形表示形式提供局部和全局架构节点（包括简单类型和复杂类型、元素、组、特性及特性组）的详细信息。

若要开始浏览感兴趣的节点，必须将它们添加到工作区中。 工作区在所有视图之间共享。

## <a name="add-nodes-to-the-workspace"></a>将节点添加到工作区中

可通过以下方法将节点添加到工作区中：

- 在[起始视图](../xml-tools/start-view.md)的“架构集详细信息”部分中，单击全局节点类型旁边的“添加”链接。

- 将全局节点、文件节点和命名空间节点从 XML 架构资源管理器拖放到三种视图中的任意一种视图中。 有关详细信息，请参阅 [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)中的“拖放节点”一节。

- 使用 XML 架构资源管理器中的上下文（右键单击）菜单。 有关详细信息，请参阅[上下文菜单](../xml-tools/context-menus-xml-schema-explorer.md)。

- 在 XSD 资源管理器中执行搜索，并在摘要结果窗格中单击“将突出显示的节点添加到工作区”按钮。 有关详细信息，请参阅[搜索架构集](../xml-tools/searching-the-schema-set.md)。

## <a name="switch-views"></a>切换视图

若要切换视图，请使用下列工具之一：

- XSD 设计器工具栏。

- 内容模型视图和图形视图的上下文（右键单击）菜单。

- 起始视图页上的水印、空内容模型视图上的水印或图形视图上的水印。

- 热键：Ctrl+1（起始视图）、Ctrl+2（图形视图）和 Ctrl+3（内容模型视图）。
