---
title: 依赖项关系图引用
ms.date: 09/28/2018
ms.topic: reference
f1_keywords:
- vs.teamarch.layerdiagram.layerexplorer.artifactlink
- vs.teamarch.layerdiagram.layerexplorer.artifactlink.properties
- vs.teamarch.layerdiagram.diagram
- vs.teamarch.UMLModelExplorer.layerdiagram
- vs.teamarch.layerdiagram.layerexplorer
- vs.teamarch.layerdiagram.shapes.properties
- vs.teamarch.layerdiagram.toolbox
helpviewer_keywords:
- architecture, dependency diagrams
- dependency diagrams
- diagrams - modeling, layer
- constraints, architectural
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e592b6d5da908b71aa5af9bae7afe495944301a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936782"
---
# <a name="dependency-diagrams-reference"></a>依赖项关系图： 参考

在 Visual Studio 中，你可以使用*依赖项关系图*可视化您的系统的高级别、 逻辑体系结构。 依赖项关系图将在系统中的物理项目组织到名为的逻辑抽象组*层*。 这些层用于描述这些项目执行的主要任务或系统的主要组件。 每一层还可以包含描述更详细的任务的嵌套层。

若要查看哪些版本的 Visual Studio 支持此功能，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

> [!NOTE]
> 不支持在 Visual Studio 中的.NET Core 项目的依赖项关系图。

你可以指定各层之间的预期或现有依赖项。 这些依赖项（表示为箭头）指示哪些层可以使用或当前正在使用由其他层表示的功能。 通过将系统组织到描述不同的角色和功能的层，依赖项关系图可以帮助使你更轻松地理解、 重用和维护你的代码。

使用依赖项关系图来帮助你执行以下任务：

- 传达系统的现有或预期逻辑体系结构。

- 发现现有代码和预期体系结构之间的冲突。

- 在重构、更新或改进你的系统时，可视化更改对预期体系结构的影响。

- 在开发和维护你的代码过程中，通过包括对签入的验证来强化预期体系结构并生成操作。

本主题介绍了可以使用依赖项关系图上的元素。 有关更多详细信息，有关如何创建和绘制依赖项关系图，请参阅[依赖项关系图：指导原则](../modeling/layer-diagrams-guidelines.md)。 有关分层模式的详细信息，请访问[模式和实践站点](http://go.microsoft.com/fwlink/?LinkId=145794)。

## <a name="reading-dependency-diagrams"></a>读取依赖项关系图

![依赖项关系图上的元素](../modeling/media/uml_layerrefreading.png)

下表描述了可以使用依赖项关系图上的元素。

|**Shape**|**元素**|**说明**|
|-|-|-|
|1|**层**|系统中的物理项目的逻辑组。 这些项目可以是命名空间、项目、类、方法等。<br /><br /> 若要查看链接到某个层的项目，打开层的快捷菜单，然后选择**查看链接**以打开**层资源管理器**。<br /><br /> 有关详细信息，请参阅[层资源管理器](#Explorer)。<br /><br /> -   **禁止 Namespace 依赖项**-指定与此层相关联的项目不能依赖于指定的命名空间。<br />-   **禁止的命名空间**-指定与此层相关联的项目不得属于指定的命名空间。<br />-   **所需的命名空间**-指定与此层相关联的项目必须属于某个指定的命名空间。|
|2|**依赖关系**|指示某个层可以使用另一层的功能，但反之则不然。<br /><br /> -   **方向**-指定依赖项的方向。|
|3|**双向依赖项**|指示某个层可以使用另一层的功能，反之易然。<br /><br /> -   **方向**-指定依赖项的方向。|
|4|**注释**|用于将一般注释添加到关系图或关系图上的元素。|
|5|**注释链接**|用于将注释链接到关系图上的元素。|

## <a name="Explorer"></a> 层资源管理器

在解决方案中，如项目、类、命名空间、项目文件和软件的其他部件，你可以将每个层链接到项目。 层上的数字显示链接到该层的项目数。 但是，在读取层上的项目数时，请记住：

- 如果某个层链接到一个包含其他项目的项目，但该层未直接链接到其他项目，则该数字仅包括链接的项目。 但是，在层验证过程中其他项目包括在分析范围内。

     例如，如果一个层链接到单个命名空间，则链接的项目数是 1，即使该命名空间包含类也是如此。 如果该层还链接到命名空间中的每个类，则该数字将包括链接的类。

- 如果一个层包含链接到项目的其他层，则容器层也链接到这些项目，即使容器层上的数字不包括这些项目。

有关链接层和项目的详细信息，请参阅：

- [依赖项关系图：指南](../modeling/layer-diagrams-guidelines.md)

- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)

### <a name="examine-the-linked-artifacts"></a>检查链接的项目

在依赖项关系图中，打开一个或多个层的快捷菜单，然后选择**查看链接**。

**层资源管理器**将打开并显示链接到所选层的项目。 **层资源管理器**有一列显示了每个项目链接的属性。

> [!NOTE]
> 如果您不能查看所有这些属性，请展开**层资源管理器**窗口。

|**层资源管理器中的列**|**说明**|
|-|-|
|**类别**|项目种类，例如类、命名空间、源文件等|
|**层**|链接到该项目的层|
|**支持验证**|如果 **，则返回 True**，则层验证过程可以验证项目是否符合指向或来自此元素的依赖关系。<br /><br /> 如果**False**，则该链接不参与层验证过程。<br /><br /> 有关详细信息，请参阅[依赖项关系图：指导原则](../modeling/layer-diagrams-guidelines.md)。|
|标识符|对链接的项目的引用|

## <a name="see-also"></a>请参阅

- [为应用程序创建模型](../modeling/create-models-for-your-app.md)
