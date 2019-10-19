---
title: XML 架构资源管理器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 2fc39e98-b194-456b-a452-cfafb0a52d66
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5e9f61c56dd7ff2a9c6c19afc20ed279a7fdf855
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669376"
---
# <a name="xml-schema-explorer"></a>XML 架构资源管理器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML 架构资源管理器与 Microsoft Visual Studio 和 XML 编辑器相集成，从而使您可以使用 XML 架构定义语言 (XSD) 架构。 打开 XML 架构文件时，"**架构集**" 节点将显示在 "Xml 架构资源管理器" 中。 目标文件的所有包含架构、导入架构或重新定义的架构，以及通过 `include` 或 `import` 语句引用的任何文件，也出现在 XML 架构资源管理器中。

 使用 XML 架构资源管理器，您可以执行下列操作：

- 快速了解架构集。

- 浏览和导航树。

- 执行关键字搜索和架构特定的搜索。 有关详细信息，请参阅[搜索架构集](../xml-tools/searching-the-schema-set.md)。

- 向图形视图或内容模型视图添加搜索结果

- 按文档顺序、类型或名称对树进行排序。 有关详细信息，请参阅[排序、筛选和分组](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)。

- 打开 XML 编辑器，然后跳到 XSD 文件中的代码位置。 有关详细信息，请参阅[与 XML 编辑器集成](../xml-tools/integration-with-xml-editor.md)。

- 为全局元素生成示例 XML。

  XML 架构资源管理器通过树视图提供架构集的分层视图。 XML 架构资源管理器还提供搜索、筛选、导航和排序功能。 若要访问 XML 架构资源管理器，请执行下列操作之一：

- 如果在 "开始"[视图](../xml-tools/start-view.md)中，请单击 " **XML 架构资源管理器**" 链接。

- 如果在[图形视图](../xml-tools/graph-view.md)或[内容模型视图](../xml-tools/content-model-view.md)中，并在工作区中包含节点，请使用上下文菜单选择 "XML 架构资源管理器"。

- 还可以在 "**视图**" 菜单中选择 "XML 架构 Explorerfrom"。

- 可以访问 XML 架构 Explorerfrom，其中包含与 .xsd 文件相关联的 Visual Basic XML 文本。 若要在 XML 架构资源管理器中查看架构集，请右键单击 XML 文本或 XML 命名空间导入中的 XML 节点，然后选择 "**在架构资源管理器中显示**" 命令。 有关详细信息，请参阅将[Xml 文本与 Xml 架构资源管理器集成](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)。

## <a name="tree-view"></a>树视图
 XML 架构资源管理器以树结构显示预编译的架构集信息。 树结构的组织方式如下：

- 位于顶级的是架构集节点。

- 第二级中包含命名空间。

- 第三级中包含文件。

- 第四级中包含全局节点， 其中可包括元素、组、复杂类型、简单类型、特性、特性组以及 `include`、`import` 和 `redefine` 语句。

  下面是树结构的示例：

  ![XML 架构资源管理器](../xml-tools/media/xmlschemaexplorer.gif "XMLSchemaExplorer")

## <a name="selection-and-activation"></a>选择和激活
 若要突出显示并选择节点，请在架构资源管理器中单击一次。

 若要激活某个节点，请双击该节点或在该节点处于选定状态时按**enter** 。

- 激活某节点时会打开在其中定义该节点的文件（如果文件尚未打开）并在文件中选择该节点。

- 激活文件节点时会打开选定文件（如果该文件尚未打开）并突出显示 `<schema>` 节点。

- 激活架构集或命名空间节点不会执行任何操作。

## <a name="draging-and-dropping-nodes"></a>拖放节点
 可以将全局节点、文件节点和命名空间节点拖放到 XSD 设计器视图上。 如果当前视图是[起始视图](../xml-tools/start-view.md)，则将上的节点拖动到该视图将打开[图形视图](../xml-tools/graph-view.md)。 如果当前视图是 "[内容模型视图](../xml-tools/content-model-view.md)" 或 "图形" 视图，则在将节点拖放到该视图时，视图不会更改。

 删除视图中的文件会将该文件中的所有全局节点添加到[XSD 设计器工作区](../xml-tools/xml-schema-designer-workspace.md)。 将命名空间放置在视图上将向工作区添加命名空间中的所有全局节点。 工作区在所有视图之间共享。

 不能拖放或导入本地节点。

## <a name="in-this-section"></a>本节内容

- [搜索架构集](../xml-tools/searching-the-schema-set.md)

- [排序、筛选和分组](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)

- [上下文菜单](../xml-tools/context-menus-xml-schema-explorer.md)

- [XML 文本与 XML 架构资源管理器的集成](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)

## <a name="see-also"></a>请参阅
 [如何：从 XML 架构资源管理器向工作区添加节点](../xml-tools/how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer.md)
