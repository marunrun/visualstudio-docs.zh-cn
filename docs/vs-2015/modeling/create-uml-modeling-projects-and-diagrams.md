---
title: Create UML modeling projects and diagrams | Microsoft Docs
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
ms.openlocfilehash: d5884dcd3f9e3cb8f1910d2e23ec80f910ed2fc9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301003"
---
# <a name="create-uml-modeling-projects-and-diagrams"></a>创建 UML 建模项目和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML 模型的有助于你了解、讨论和设计软件系统。 Visual Studio 为五种最常用的 UML 关系图提供了模板：活动、类、组件、序列和用例。 此外，你可以创建层关系图，这将帮助你定义你的系统的结构。

 UML 建模图和层关系图只可以存在于建模项目内。 每个建模项目包含一个共享的 UML 模型和几个 UML 关系图。 每个关系图是模型的部分视图。 UML 模型包含在 UML 关系图上的所有元素，并可以使用 UML 模型资源管理器来查看。 For information about models and their relationship to diagrams, see [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md). For information about modeling projects under version control, see [Manage models and diagrams under version control](../modeling/manage-models-and-diagrams-under-version-control.md) and [Structure your modeling solution](../modeling/structure-your-modeling-solution.md)

> [!NOTE]
> 还有另一种关系图，即 .NET 类关系图，它用于可视化程序代码。 For more information, see [Designing and Viewing Classes and Types](https://go.microsoft.com/fwlink/?LinkId=142231).

## <a name="CreatingModelingDiagrams"></a> Create a Diagram in a Modeling Project
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

#### <a name="to-create-a-diagram-and-add-it-to-a-project"></a>若要创建关系图并将其添加到项目中

1. On the **Architecture** menu, choose **New UML or Layer Diagram**.

2. In the **Add New Diagram** dialog box, click the type of modeling diagram that you want.

    ![Add New Diagram dialog](../modeling/media/uml-adddiagram.png "UML_AddDiagram")

3. 为新关系图键入名称。

4. In the **Add to modeling project** box:

   - Select a modeling project that already exists in your solution, and then click **OK**.

     \- 或 -

   1. Select **Create a new modeling project**, and then click **OK**.

   2. In the **Create New Modeling Project** dialog box, type a name and location for the new project, and then click **OK**.

        ![Create New Modeling Project dialog](../modeling/media/uml-createmodel.png "UML_CreateModel")

        如果你的解决方案已打开，新的项目被添加到解决方案中。 如果你没有打开解决方案，你可以为新解决方案键入名称。

   如果你已经有一个建模项目，你还可以使用以下过程。

#### <a name="to-add-a-diagram-to-an-existing-modeling-project"></a>若要将关系图添加到现有建模项目中

1. In **Solution Explorer**, click the modeling project node.

    > [!NOTE]
    > The modeling project contains a model definition folder named **ModelDefinition**.

2. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

3. In the **Add New Item -** *\<project name>* dialog box, under **Templates**, click the modeling diagram type, for example, **UML Component Diagram**.

4. Type a name for the diagram, and then click **Add**.

     建模图将打开并显示在建模项目中。

    > [!CAUTION]
    > 请勿添加、复制或将现有的关系图文件拖动到其他建模项目或解决方案中的其他位置。 这使元素从复制的关系图中消失或在你打开关系图时发生错误。 你必须从在其中创建的建模项目中打开关系图文件。 这是因为 UML 关系图是由其建模项目拥有的模型视图。 若要复制一个关系图文件，请创建一个新的关系图，然后将源关系图中的元素复制到新关系图中。 For more information, see [Troubleshooting Modeling Projects and Diagrams](#TroubleshootingModelingProjects).

#### <a name="to-create-a-blank-modeling-project"></a>要创建空白建模项目

1. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

2. In the **New Project** dialog box, under **Installed Templates**, click **Modeling Projects**.

3. In the middle window, click **Modeling Project**.

4. Name the project and specify a location in the **Name** and **Location** boxes.

5. In the **Solution** box, select **Add to Solution** to add the new project to a solution you already have open; or **Create new Solution** to close any open solution and add the project to a new solution.

## <a name="RemovingModelingDiagrams"></a> Removing Modeling Diagrams from a Project
 你可以永久删除关系图，或你可暂时从项目中排除一个关系图，然后恢复它。

#### <a name="to-permanently-delete-a-diagram-from-a-project"></a>若要从项目中永久删除关系图

- In **Solution Explorer**, right-click the main file that represents the diagram, and then click **Delete**.

     从项目和文件系统中删除该关系图。 The elements shown on the diagram are not removed from **UML Model Explorer**.

    > [!NOTE]
    > 每个关系图有两个文件，一个附属于另一个。 例如，如果你有一个名为`CD1`的组件关系图，你应该删除名为`CD1.componentdiagram`的文件。 名为`CD1.componentdiagram.layout`的附属文件将被自动删除。

#### <a name="to-temporarily-exclude-a-diagram-from-a-project"></a>若要暂时从项目中排除一个关系图

- In **Solution Explorer**, right-click the diagram file, and then click **Exclude from Project**.

     该关系图从项目中移除。 它不是从文件系统中删除。

    > [!NOTE]
    > The elements shown on the diagram are not removed from **UML Model Explorer**.

#### <a name="to-restore-a-temporarily-excluded-diagram-to-a-project"></a>若要把临时排除的关系图还原到项目中

1. In **Solution Explorer**, click the modeling project node.

    > [!NOTE]
    > The modeling project contains a model definition folder named **ModelDefinition**.

2. On the **Project** menu, click **Add Existing Item**.

3. In the **Add Existing Item** dialog box, locate the diagram file, select the file, and then click **Add**.

     建模图将打开并显示在建模项目中。

    > [!NOTE]
    > 每个关系图都包含文件系统中的一对文件。 不要选择扩展名为 `.layout` 的文件。 此外，Visual Studio 不支持将现有的 UML 关系图添加到多个建模项目中。 必须在其创建的建模项目中打开每个关系图文件。 这是因为 UML 关系图将显示其建模项目拥有的模型的视图。

## <a name="NonModelDiagrams"></a> Diagrams that Do Not Require Modeling Projects
 以下类型的关系图不是一个建模项目的一部分：

- 作为源代码的视图创建的类图。 这些与 UML 类图不相关。 For more information, see [Designing and Viewing Classes and Types](../ide/designing-and-viewing-classes-and-types.md).

- 代码映射。 请参阅 [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md)。

- 关系图不是 UML 关系图或层关系图，如域特定语言。

## <a name="TroubleshootingModelingProjects"></a> Troubleshooting Modeling Projects and Diagrams
 下表介绍了建模项目或关系图可能出现的问题以及如何解决这些问题：

|**问题**|**Causes**|**解决方法**|
|---------------|----------------|--------------------|
|建模项目无法打开或加载到解决方案中。<br /><br /> 显示以下消息：<br /><br /> “解决方案中的一个或多个项目未能正确加载。 请参阅输出窗口获取有关的详细信息。”<br /><br /> 输出窗口将显示以下消息：<br /><br /> "*ModelingProjectFilenameAndPath*.modelproj: error: Unrecognized Guid format."|建模项目引用的项目名称相同，而且在相同的解决方案中。<br /><br /> 例如，一个层链接到名称相同的项目中，而且它们在相同的解决方案中。|使用文本编辑器打开建模项目文件并删除引用，然后尝试再次打开该建模项目。<br /><br /> 若要避免此问题，不要添加对具有相同名称的项目的引用。 请确保项目具有唯一的名称。|
|元素从添加、复制或拖放到其他建模项目或解决方案中其他位置的关系图中丢失。<br /><br /> - 或 -<br /><br /> 当你尝试打开关系图时，将显示以下消息：<br /><br /> -   "Some shapes or connectors on the diagram are missing because their definitions do not exist in this project. 关系图关闭时定义已从模型中删除，或关系图被复制到另一个不包含这些定义的项目中。”<br /><br /> - 或 -<br /><br /> -   "This document is opened by another project."|关系图文件或从建模项目添加、拖动或复制到另一个建模项目或解决方案中的另一个位置。|若要复制一个关系图文件，请创建一个新的关系图，然后将源关系图中的元素复制到新关系图中。|

## <a name="see-also"></a>请参阅
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [Structure your modeling solution](../modeling/structure-your-modeling-solution.md)
