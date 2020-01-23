---
title: 创建 UML 建模项目和关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.addnewdiagramdialog
- vs.teamarch.createnewmodelingprojectdialog
helpviewer_keywords:
- projects [Visual Studio ALM], modeling
- diagrams - modeling, modeling
- modeling diagrams
- projects, UML
- UML, deleting diagrams
- UML
- UML diagrams, adding
- UML, projects
- Visual Studio ALM, modeling projects
- modeling projects
- UML diagrams
- projects, modeling
ms.assetid: c178b04b-4fd2-4bed-97e3-d793dae8649c
caps.latest.revision: 50
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 52c55b2cfdf000d91a83071b53e8e9450187b720
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852022"
---
# <a name="create-uml-modeling-projects-and-diagrams"></a>创建 UML 建模项目和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML 模型的有助于你了解、讨论和设计软件系统。 Visual Studio 为五种最常用的 UML 关系图提供了模板：活动、类、组件、序列和用例。 此外，你可以创建层关系图，这将帮助你定义你的系统的结构。

 UML 建模图和层关系图只可以存在于建模项目内。 每个建模项目包含一个共享的 UML 模型和几个 UML 关系图。 每个关系图是模型的部分视图。 UML 模型包含在 UML 关系图上的所有元素，并可以使用 UML 模型资源管理器来查看。 有关模型及其与关系图的关系的信息，请参阅[编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)。 有关版本控制下的建模项目的信息，请参阅[管理版本控制下的模型和关系图](../modeling/manage-models-and-diagrams-under-version-control.md)并[构建建模解决方案](../modeling/structure-your-modeling-solution.md)

> [!NOTE]
> 还有另一种关系图，即 .NET 类关系图，它用于可视化程序代码。 有关详细信息，请参阅[设计和查看类和类型](https://msdn.microsoft.com/library/ab7aty24.aspx)。

## <a name="CreatingModelingDiagrams"></a>在建模项目中创建关系图
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

#### <a name="to-create-a-diagram-and-add-it-to-a-project"></a>若要创建关系图并将其添加到项目中

1. 在 "**体系结构**" 菜单上，选择 "**新建 UML 或层关系图**"。

2. 在 "**添加新关系图**" 对话框中，单击所需的建模图类型。

    !["添加新关系图" 对话框](../modeling/media/uml-adddiagram.png "UML_AddDiagram")

3. 为新关系图键入名称。

4. 在 "**添加到建模项目**" 框中：

   - 选择解决方案中已存在的建模项目，然后单击 **"确定"** 。

     \- 或 -

   1. 选择 "**创建新的建模项目**"，然后单击 **"确定"** 。

   2. 在 "**创建新的建模项目**" 对话框中，键入新项目的名称和位置，然后单击 **"确定"** 。

        !["创建新建模项目" 对话框](../modeling/media/uml-createmodel.png "UML_CreateModel")

        如果你的解决方案已打开，新的项目被添加到解决方案中。 如果你没有打开解决方案，你可以为新解决方案键入名称。

   如果你已经有一个建模项目，你还可以使用以下过程。

#### <a name="to-add-a-diagram-to-an-existing-modeling-project"></a>若要将关系图添加到现有建模项目中

1. 在**解决方案资源管理器**中，单击 "建模项目" 节点。

    > [!NOTE]
    > 建模项目包含一个名为**ModelDefinition**的模型定义文件夹。

2. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

3. 在 "**添加新项-** *\<项目名称 >* " 对话框中的 "**模板**" 下，单击建模图类型，例如 " **UML 组件图**"。

4. 键入关系图的名称，然后单击 "**添加**"。

     建模图将打开并显示在建模项目中。

    > [!CAUTION]
    > 请勿添加、复制或将现有的关系图文件拖动到其他建模项目或解决方案中的其他位置。 这使元素从复制的关系图中消失或在你打开关系图时发生错误。 你必须从在其中创建的建模项目中打开关系图文件。 这是因为 UML 关系图是由其建模项目拥有的模型视图。 若要复制一个关系图文件，请创建一个新的关系图，然后将源关系图中的元素复制到新关系图中。 有关详细信息，请参阅[排查建模项目和关系图](#TroubleshootingModelingProjects)。

#### <a name="to-create-a-blank-modeling-project"></a>要创建空白建模项目

1. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

2. 在 "**新建项目**" 对话框中的 "**已安装的模板**" 下，单击 "**建模项目**"。

3. 在中间窗口中，单击 "**建模项目**"。

4. 命名项目，并在 "**名称**" 和 "**位置**" 框中指定一个位置。

5. 在 "**解决方案**" 框中，选择 "**添加到解决方案**" 将新项目添加到已打开的解决方案;或**创建新解决方案**来关闭任何打开的解决方案，并将项目添加到新的解决方案中。

## <a name="RemovingModelingDiagrams"></a>从项目中删除建模图
 你可以永久删除关系图，或你可暂时从项目中排除一个关系图，然后恢复它。

#### <a name="to-permanently-delete-a-diagram-from-a-project"></a>若要从项目中永久删除关系图

- 在**解决方案资源管理器**中，右键单击表示关系图的主文件，然后单击 "**删除**"。

     从项目和文件系统中删除该关系图。 关系图上显示的元素不会从**UML 模型资源管理器**中删除。

    > [!NOTE]
    > 每个关系图有两个文件，一个附属于另一个。 例如，如果你有一个名为`CD1`的组件关系图，你应该删除名为`CD1.componentdiagram`的文件。 名为`CD1.componentdiagram.layout`的附属文件将被自动删除。

#### <a name="to-temporarily-exclude-a-diagram-from-a-project"></a>若要暂时从项目中排除一个关系图

- 在**解决方案资源管理器**中，右键单击关系图文件，然后单击 "**从项目中排除**"。

     该关系图从项目中移除。 它不是从文件系统中删除。

    > [!NOTE]
    > 关系图上显示的元素不会从**UML 模型资源管理器**中删除。

#### <a name="to-restore-a-temporarily-excluded-diagram-to-a-project"></a>若要把临时排除的关系图还原到项目中

1. 在**解决方案资源管理器**中，单击 "建模项目" 节点。

    > [!NOTE]
    > 建模项目包含一个名为**ModelDefinition**的模型定义文件夹。

2. 在“项目”菜单上，单击“添加现有项”。

3. 在 "**添加现有项**" 对话框中，找到该关系图文件，选择该文件，然后单击 "**添加**"。

     建模图将打开并显示在建模项目中。

    > [!NOTE]
    > 每个关系图都包含文件系统中的一对文件。 不要选择扩展名为 `.layout` 的文件。 此外，Visual Studio 不支持将现有的 UML 关系图添加到多个建模项目中。 必须在其创建的建模项目中打开每个关系图文件。 这是因为 UML 关系图将显示其建模项目拥有的模型的视图。

## <a name="NonModelDiagrams"></a>不需要建模项目的关系图
 以下类型的关系图不是一个建模项目的一部分：

- 作为源代码的视图创建的类图。 这些与 UML 类图不相关。 有关详细信息，请参阅[设计和查看类和类型](../ide/designing-and-viewing-classes-and-types.md)。

- 代码映射。 请参阅 [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md)。

- 关系图不是 UML 关系图或层关系图，如域特定语言。

## <a name="TroubleshootingModelingProjects"></a>建模项目和关系图疑难解答
 下表介绍了建模项目或关系图可能出现的问题以及如何解决这些问题：

|**问题**|**导致**|**解决方法**|
|---------------|----------------|--------------------|
|建模项目无法打开或加载到解决方案中。<br /><br /> 显示以下消息：<br /><br /> “解决方案中的一个或多个项目未能正确加载。 请参阅输出窗口获取有关的详细信息。”<br /><br /> 输出窗口将显示以下消息：<br /><br /> "*ModelingProjectFilenameAndPath*： .modelproj：错误：无法识别的 Guid 格式。"|建模项目引用的项目名称相同，而且在相同的解决方案中。<br /><br /> 例如，一个层链接到名称相同的项目中，而且它们在相同的解决方案中。|使用文本编辑器打开建模项目文件并删除引用，然后尝试再次打开该建模项目。<br /><br /> 若要避免此问题，不要添加对具有相同名称的项目的引用。 请确保项目具有唯一的名称。|
|元素从添加、复制或拖放到其他建模项目或解决方案中其他位置的关系图中丢失。<br /><br /> -或者-<br /><br /> 当你尝试打开关系图时，将显示以下消息：<br /><br /> -缺少关系图上的某些形状或连接符，因为此项目中不存在其定义。 关系图关闭时定义已从模型中删除，或关系图被复制到另一个不包含这些定义的项目中。”<br /><br /> -或者-<br /><br /> -"此文档由另一个项目打开。"|关系图文件或从建模项目添加、拖动或复制到另一个建模项目或解决方案中的另一个位置。|若要复制一个关系图文件，请创建一个新的关系图，然后将源关系图中的元素复制到新关系图中。|

## <a name="see-also"></a>请参阅
 [编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)[构建建模解决方案](../modeling/structure-your-modeling-solution.md)
