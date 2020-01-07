---
title: XML 架构资源管理器
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 2fc39e98-b194-456b-a452-cfafb0a52d66
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 04c6415fed131abc5a102f6ec15c69e33f21fd68
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592342"
---
# <a name="xml-schema-explorer"></a>XML 架构资源管理器

**Xml 架构资源管理器**与 MICROSOFT VISUAL STUDIO 和 xml 编辑器集成，使您能够使用 xml 架构定义语言（XSD）架构。 打开 XML 架构文件时，"**架构集**" 节点将显示在 " **Xml 架构资源管理器**" 中。 你的目标文件的所有包含的、导入或重新定义的架构，以及通过 `include` 或 `import` 语句引用的所有文件也会显示在**XML 架构资源管理器**中。

**XML 架构资源管理器**使您能够执行以下操作：

- 快速了解架构集。

- 浏览和导航树。

- 执行关键字搜索和架构特定的搜索。 有关详细信息，请参阅[搜索架构集](../xml-tools/searching-the-schema-set.md)。

- 将搜索结果添加到图形视图或内容模型视图

- 按文档顺序、类型或名称对树进行排序。 有关详细信息，请参阅[排序、筛选和分组](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)。

- 打开 XML 编辑器，跳转到 XSD 文件中的代码位置。 有关详细信息，请参阅[与 XML 编辑器集成](../xml-tools/integration-with-xml-editor.md)。

- 为全局元素生成示例 XML。

**XML 架构资源管理器**通过树视图提供架构集的层次结构视图。 **XML 架构资源管理器**还提供搜索、筛选、导航和排序功能。 若要访问**XML 架构资源管理器**，请执行以下操作之一：

- 如果在 "开始"[视图](../xml-tools/start-view.md)中，请单击 " **XML 架构资源管理器**" 链接。

- 如果你在[图形视图](../xml-tools/graph-view.md)或[内容模型视图](../xml-tools/content-model-view.md)中，并在工作区中包含节点，请使用上下文（右键单击）菜单选择**XML 架构资源管理器**。

- 你还可以从 "**视图**" 菜单中选择 " **XML 架构资源管理器**"。

- 你可以从一个 *.vb*文件访问**Xml 架构资源管理器**，该文件具有与 *.xsd*文件相关联的 Visual Basic XML 文本。 若要在**Xml 架构资源管理器**中查看架构集，请右键单击 xml 文本或 xml 命名空间导入中的 xml 节点，然后选择 "**在架构资源管理器中显示**" 命令。 有关详细信息，请参阅将[xml 文本与 Xml 架构资源管理器集成](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)。

## <a name="tree-view"></a>树视图
**XML 架构资源管理器**在树结构中显示预编译的架构集信息。 树结构的组织方式如下：

- 位于顶级的是架构集节点。

- 第二级中包含命名空间。

- 第三级中包含文件。

- 第四级中包含全局节点， 其中可包括元素、组、复杂类型、简单类型、特性、特性组以及 `include`、`import` 和 `redefine` 语句。

下面是树结构的示例：

![XML 架构资源管理器](../xml-tools/media/xmlschemaexplorer.gif)

## <a name="selection-and-activation"></a>选择和激活
若要突出显示并选择节点，请在架构资源管理器中单击一次。

若要激活某个节点，请双击该节点或在该节点处于选定状态时按**enter** 。

- 激活某节点时会打开在其中定义该节点的文件（如果文件尚未打开）并在文件中选择该节点。

- 激活文件节点时会打开选定文件（如果该文件尚未打开）并突出显示 `<schema>` 节点。

- 激活架构集或命名空间节点不会执行任何操作。

## <a name="drag-and-drop-nodes"></a>拖放节点
可以将全局节点、文件节点和命名空间节点拖放到 XSD 设计器视图上。 如果当前视图是[起始视图](../xml-tools/start-view.md)，则将上的节点拖动到该视图将打开[图形视图](../xml-tools/graph-view.md)。 如果当前视图是 "[内容模型视图](../xml-tools/content-model-view.md)" 或 "图形" 视图，则在将节点拖放到该视图时，视图不会更改。

删除视图中的文件会将该文件中的所有全局节点添加到[XSD 设计器工作区](../xml-tools/xml-schema-designer-workspace.md)。 将命名空间放置在视图上将向工作区添加命名空间中的所有全局节点。 工作区在所有视图之间共享。

 不能拖放或导入本地节点。

## <a name="see-also"></a>另请参阅

- [如何：从 XML 架构资源管理器将节点添加到工作区](../xml-tools/how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer.md)
