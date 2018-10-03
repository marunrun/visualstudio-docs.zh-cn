---
title: 编辑 UML 模型和关系图 |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.modelingproject
- vs.teamarch.UMLModelExplorer
- vs.teamarch.UMLModelExplorer.rootnode
helpviewer_keywords:
- diagrams - modeling
- UML, copy and paste
- UML, models
- UML model
- UML, element properties
- UML
- UML, diagrams
ms.assetid: 87affd40-8127-4ee9-9d3a-ad977abe2ed6
caps.latest.revision: 86
author: alexhomer1
ms.author: gewarren
manager: douge
ms.openlocfilehash: 0620f0a1212d7abd864a9428492d95067098ef16
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47477921"
---
# <a name="edit-uml-models-and-diagrams"></a>编辑 UML 模型和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[编辑 UML 模型和关系图](https://docs.microsoft.com/visualstudio/modeling/edit-uml-models-and-diagrams)。  
  
可以通过由多种不同类型的关系图提供的视图创建和编辑 UML 模型。 通过在你的系统上提供不同的透视图，这些关系图有助于了解和讨论设计和需求的不同方面。 Visual Studio 提供了五种最常用的 UML 关系图模板。  
  
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
 本主题介绍了用于编辑在不同的关系图类型之中共有的模型的方法。 特定于特定类型的关系图的详细信息，请参阅[为您的应用程序创建模型](../modeling/create-models-for-your-app.md)。  
  
## <a name="in-this-topic"></a>本主题内容  
  
-   [UML 关系图是 UML 模型的视图](#Views)  
  
-   [创建 UML 建模图](#Creating)  
  
-   [绘制 UML 建模关系图](#Drawing)  
  
-   [编辑形状和连接线](#Editing)  
  
-   [对模型撤消更改](#Undo)  
  
-   [关系图之间共享元素](#Sharing)  
  
-   [复制元素和相关元素的组](#Copying)  
  
-   [删除模型元素或其视图](#Deleting)  
  
-   [在关系图中搜索文本](#Searching)  
  
-   [为演示文稿准备一个关系图](#presentation)  
  
-   [扩展 UML 设计器](#extensions)  
  
##  <a name="Views"></a> UML 关系图是 UML 模型的视图  
 只能在建模项目中创建和使用 UML 关系图。 有关如何创建关系图和项目的详细信息，请参阅[创建 UML 建模项目和关系图](../modeling/create-uml-modeling-projects-and-diagrams.md)。  
  
-   一个建模项目只包含一个 UML 模型。 项目中的每个 UML 关系图都是 UML 模型视图。  
  
-   您可以查看在模型**UML 模型资源管理器**。 上**体系结构**菜单，依次指向**Windows**，然后单击**UML 模型资源管理器**。  
  
-   关系图上的每个形状都是模型中元素的视图。 当将新形状置于关系图上时，将在模型中创建一个新元素。  
  
-   当保存任何关系图，Visual Studio 将保存整个模型时，其所有关系图以及建模项目文件。  
  
##  <a name="Creating"></a> 创建 UML 建模图  
  
1.  上**体系结构**菜单上，在 Visual Studio 中，单击**新建 UML 或层关系图**。  
  
2.  选择并命名关系图。  
  
3.  在中**将添加到建模项目**中，选择一个现有建模项目，或选择**创建一个新建模项目**。  
  
    > [!NOTE]
    >  建模关系图必须存在于建模项目内。  
  
 还可以向解决方案资源管理器中的一个现有的建模项目添加关系图。 右键单击建模项目，指向**外**，然后单击**新项**。  
  
#### <a name="to-create-an-empty-uml-modeling-project"></a>若要创建空的 UML 建模项目  
  
-   上**文件**菜单，依次指向**新建**，单击**项目**，然后在**新项目**对话框中，双击**建模项目**。  
  
 有关如何管理建模项目的详细信息，请参阅[创建 UML 建模项目和关系图](../modeling/create-uml-modeling-projects-and-diagrams.md)。  
  
##  <a name="Drawing"></a> 绘制 UML 建模关系图  
 建模图显示通过关系链接的模型元素集合。 每个元素显示为一个形状，每个关系显示为两个形状之间的连接线。  
  
 有两种类型的工具，一种用于元素，另一种用于关系。 例如，在 UML 类图工具箱中，**类**是一种元素工具，并**关联**是一种关系工具。  
  
> [!NOTE]
>  如果您需要特定于特定关系图类型的信息，请参阅[为您的应用程序创建模型](../modeling/create-models-for-your-app.md)。  
  
#### <a name="to-create-elements-and-relationships-in-a-uml-modeling-diagram"></a>若要在 UML 建模关系图中创建元素和关系  
  
1.  若要创建模型元素，则单击“工具箱”中的元素工具，然后单击希望元素在其中进行显示的关系图。 创建该元素后，通过拖动其句柄调整其大小和形状。  
  
     在某些情况下，可以将新元素放置在另一个元素内。 例如，在 UML 类关系图上，可以将类放置在包内。  
  
    > [!NOTE]
    >  如果无法看到工具箱中，单击**工具箱**上**视图**菜单。  
  
2.  若要创建关系，则单击关系工具，单击想要关系从其开始的元素，然后单击想要关系以其结束的元素。  
  
     不同类型的关系可以在不同类型的元素上启动或结束。 例如，在 UML 类关系图中，关联关系不能在 Comment 元素上开始或结束。  
  
    > [!NOTE]
    >  若要多次使用同一个工具，请双击该工具。 完成后，单击**指针**工具。  
  
 在某些类型的关系图上，还可以绘制简单的形状。 这些形状不是模型的一部分，但你可以使用它们强调部分关系图或将其分成不同的区域。  
  
##  <a name="Editing"></a> 编辑形状和连接线  
 当调整形状大小或给形状涂色，或者重新布局连接线时，对基础模型没有任何影响。 但是，当重命名关系图上或 UML 模型资源管理器中的形状时，将在 UML 模型资源管理器中和显示该元素的任何其他关系图中重命名相应的元素。  
  
> [!NOTE]
>  有一种创建新工具箱项的简单方法，你可以在新工具箱项中使用自选属性创建元素组或元素。 有关详细信息，请参阅[定义一个自定义建模工具箱项](../modeling/define-a-custom-modeling-toolbox-item.md)。  
  
 下图显示了如何更改形状的大小或其名称。  
  
 ![调整模型元素](../modeling/media/uml-drawadjust1.png "UML_DrawAdjust1")  
  
> [!TIP]
>  内置命令不包括用于准确对齐形状的命名。 但是，您可以轻松创建您自己的对齐方式命令代码中的示例中复制[关系图上显示 UML 模型](../modeling/display-a-uml-model-on-diagrams.md)。  
  
 下图显示了如何调整连接线及其标签的布局和位置。  
  
 ![调整连接器](../modeling/media/uml-drawadjust2.png "UML_DrawAdjust2")  
  
#### <a name="to-move-one-end-of-a-connector-to-another-shape"></a>若要将连接线的一端移动到另一个形状  
  
1.  执行下列操作之一：  
  
    -   按**CTRL**并移动该端。  
  
     \- 或 -  
  
    -   右键单击连接器，然后单击**重新连接**。  
  
2.  单击想要移动的连接线的一端。  
  
3.  单击想要将连接线移动到其中的形状。  
  
#### <a name="to-change-color-or-other-properties-of-an-element-relationship-or-diagram"></a>若要更改元素、关系或关系图的颜色或其他属性  
  
-   单击该元素并设置中的字段**属性**窗口。  
  
     如果无法看到**属性**窗口中，右键单击该元素，并单击**属性。**  
  
#### <a name="to-zoom-in-and-out-on-a-modeling-diagram"></a>若要在建模图上放大和缩小  
  
-   按下并保持**CTRL**键的同时滚动鼠标滚轮。  
  
     \- 或 -  
  
-   按下并保持**CTRL + SHIFT**，然后单击鼠标左键或右键按钮。  
  
     \- 或 -  
  
-   上**体系结构设计器**工具栏上，单击加号 (**+**) 或减号 (**-**)，或选择缩放级别。  
  
##  <a name="Searching"></a> 在关系图中搜索  
 “快速查找”功能将查找关系图上的项。 必须设置**查找：** 到**当前文档**。  
  
#### <a name="to-search-for-text-in-a-modeling-diagram"></a>若要在建模图中搜索文本  
  
1.  按**CTRL + F**。  
  
     \- 或 -  
  
     上**编辑**菜单，依次指向**查找和替换**，然后单击**快速查找**。  
  
    > [!NOTE]
    >  在中**查找和替换**对话框中，必须将保留**查找**字段设置为**当前文档**。 不支持其他选项。  
  
2.  键入你想要查找，然后单击文本**查找下一个**。  
  
    > [!NOTE]
    >  如果想要查找的文本位于折叠形状内，则将突出显示该形状。 展开该形状，然后依次**查找下一个**试。  
  
##  <a name="Undo"></a> 对模型撤消更改  
 可以撤消和重做对模型和关系图使用所做的更改**撤消**并**重做**上的命令**编辑**菜单。  
  
 **每个建模项目具有一个更改堆栈。** 对模型和关系图所做的所有更改都保留在此堆栈中。 此堆栈还包括焦点从一个关系图移动到另一个关系图的更改。 “撤消”命令可反转此堆栈上的更改。  
  
 例如，假设你执行了这些操作：对关系图 1 进行了更改；将焦点更改到关系图 2；更改了关系图 2。 撤消更改时，第一个撤销将反转最后一个更改；第二个撤消会将焦点移回到关系图 1；第三个撤消将反转对关系图 1 所做的更改。  
  
 **关闭关系图将截断更改堆栈。** 如果关闭关系图，则不能撤消在该关系图中执行的更改，并且不能撤消对模型或其任意关系图所做的早期更改。  
  
 **编辑属性时，无法撤消。** 当正在“属性”窗口或关系图上的标签中编辑属性时，仅可以撤消在该属性中所做的更改。 通过按 ENTER 键完成在属性中的更改，或按 ESC 键取消。 然后，你便可以在模型和关系图中撤消更改。  
  
 **关闭而不保存关系图可能不具有预期的效果。** 如果进行一些更改，然后关闭但没有进行保存，则所做的更改仍会保留在模型中。 如果想要关闭但不对其进行保存，则建议关闭整个模型。  
  
##  <a name="Sharing"></a> 关系图之间共享元素  
 可以将关系图中出现不止一次的模型元素作为特定实例。 这适用于类、接口、组件、用例和参与者。  
  
 如果想要在不同的关系图中显示不同组的关系，这很有用。 例如，在一个关系图中，可以显示“客户”和“地址”类之间的关联。 在另一个关系图中，可以再次显示“地址”类及其相关的邮政区域。  
  
 通过在任何关系图上选择模型元素的任何视图，或者在 UML 模型资源管理器中选择它，可以更改此模型元素的属性（例如，模型名称）。  
  
 每种关系图只能显示几种模型元素。 例如，不能在组件图上显示用例。 因此，以下过程仅适用于模型元素和关系图的某些组合。  
  
#### <a name="to-add-a-new-view-of-a-model-element-by-using-uml-model-explorer"></a>若要通过使用 UML 模型资源管理器，添加模型元素的新视图  
  
1.  若要打开**UML 模型资源管理器**，然后在**体系结构**菜单上，指向**Windows**，然后单击**UML 模型资源管理器**。  
  
2.  将从模型元素拖**UML 模型资源管理器**到同一个项目中兼容的关系图。  
  
     将显示提供模型元素的视图的形状，这可能不包括其他关系图或同一个关系图上的视图。  
  
    > [!NOTE]
    >  将类或组件拖动到序列图上时，作用是不同的。 在这种情况下，将创建一个新的生命线，其类型为该类或组件。 有关详细信息，请参阅[UML 序列图： 准则](../modeling/uml-sequence-diagrams-guidelines.md)。  
  
#### <a name="to-add-a-new-view-of-a-model-element-by-using-paste-reference"></a>若要使用“粘贴引用”添加模型元素的新视图  
  
1.  右键单击现有的元素，然后依次**复制**。  
  
    -   可以同时复制多个元素。 按住 CTRL 键同时单击每个元素中，右键单击其中一个形状，然后单击**复制**。  
  
2.  右键单击兼容关系图的空白部分，然后单击**粘贴引用**。  
  
     将显示同一元素的另一个视图。  
  
    > [!NOTE]
    >  这不同于**粘贴**命令，在模型中创建一个新元素。 有关详细信息，请参阅[复制元素和相关元素组](#Copying)。  
  
> [!NOTE]
>  如果添加到已通过关系连接的两个模型元素的关系图视图，则此关系的视图也会出现在关系图中。 只能通过从关系图删除其中一个元素或通过从模型中删除关系，来删除此视图。  
  
##  <a name="Copying"></a> 复制元素和相关元素的组  
 可以复制并粘贴模型元素，并且可以复制和粘贴元素组及其之间的关系。  
  
> [!NOTE]
>  **粘贴**并**粘贴引用**命令具有不同的效果。 **粘贴**创建新元素，其属性如下所示的复制的元素。 **粘贴引用**创建相同的元素的新视图。  
  
#### <a name="to-copy-elements-and-their-relationships"></a>若要复制的元素和它们之间的关系  
  
1.  在具有想要复制的元素的关系表中，选择一个或多个元素。  
  
    > [!NOTE]
    >  不能复制关系，除非作为组元素的一部分。  
  
2.  上**编辑**菜单上，单击**副本**。  
  
3.  如果想要将元素复制到另一个关系图，则创建新关系图，或打开现有的关系图。  
  
4.  上**编辑**菜单上，单击**粘贴**。  
  
    -   将显示元素的副本，以及任何在它们之间进行链接的关系的副本。  
  
    -   每个新元素将具有一个自动生成的新名称。  
  
5.  调整新元素和关系的位置、名称和其他属性。  
  
> [!NOTE]
>  不能将模型元素从一个模型复制到另一个模型，例如，在同一解决方案中有两个模型的情况下。 但是，可以将元素从一个关系图复制到另一个关系图。  
  
#### <a name="to-copy-an-entire-diagram"></a>若要复制整个关系图  
  
1.  创建新关系图。  
  
2.  选择现有关系图中的所有元素，复制它们，然后将其粘贴到新的关系图中。  
  
 不能通过在解决方案资源管理器中复制和粘贴，来复制关系图。  
  
##  <a name="Deleting"></a> 删除模型元素或其视图  
 可以从关系图中删除某些类型的元素（尤其是分类器），而无需从模型中进行删除。 分类器是在类图中、组件图中和用例图中显示的主要元素。 它们可以显示在多个关系图上。 对于这些类型的元素，有两个单独的命令：**从图中删除**并**从模型中删除**。  
  
 与此相反，当从关系图中删除关系时，将始终从模型中删除。  
  
> [!NOTE]
>  UML 关系图上某些类型的元素具有标签。 通过在它们周围绘制矩形来选择此类元素时，可以选择标签，而不是拥有这些标签的元素。 不支持删除以这种方式选择的元素的子集。 若要选择这些元素的子集，请按住**CTRL**键的同时单击每个元素。  
  
#### <a name="to-remove-a-classifiers-view-from-a-diagram"></a>若要从关系图删除分类器的视图  
  
-   右键单击关系图中，在元素，然后单击**从图中删除**。  
  
 \- 或 -  
  
-   单击关系图上的元素，然后按**删除**密钥。  
  
    -   元素的此视图将会消失。 但是，该元素仍保留在模型中，并且仍然可以找到它在**UML 模型资源管理器**。 任何相同元素的其他视图也将保留。  
  
    -   终止于此形状的每个连接线将从关系图中删除，但其代表的关系将保留在模型中。 可以查看中的关系**UML 模型资源管理器**下**关系**，它将连接每个元素下。  
  
#### <a name="to-delete-an-element-from-the-model"></a>若要从模型中删除元素  
  
-   或者右键单击该元素中**UML 模型资源管理器**或关系图中，，然后单击**从模型中删除**。  
  
    -   该元素将从显示它的每个关系图中删除。  
  
    -   终止于此元素的每个关系也将从模型中删除。  
  
#### <a name="to-delete-a-relationship-from-the-model"></a>若要从模型中删除关系  
  
-   右键单击关系图上或在**UML 模型资源管理器**，然后单击**从模型中删除**。  
  
    > [!CAUTION]
    >  在没有将关系从模型中删除的情况下，则不能从关系图中删除该关系。  
  
     该关系将从模型中删除，并且将从显示它的每个关系图中删除。  
  
##  <a name="presentation"></a> 为演示文稿准备一个关系图  
 以下功能有助于强调关系图的特定部分、添加说明或将关系图划分为不同感兴趣的区域。  
  
-   可以将关系图的任何部分复制到 Word、PowerPoint 或其他文档中。 选择形状和连接线想，右键单击，然后单击**复制**。  
  
-   可以更改任何形状或连接线的颜色。 选择一个或多个形状并将更改**颜色**属性。 如果看不到“属性”窗口，请按“F4”。  
  
-   可以在某些种类的关系图上绘制线条、 矩形和从省略号**简单形状**工具箱的部分。 这些形状并不构成 UML 模型的一部分。  
  
-   若要为区域添加标签，可以从工具箱拖动注释，然后设置其**Transparent**属性设置为**True**。 就像“简单形状”一样，注释不构成 UML 模型的一部分，并且不会显示在 UML 模型资源管理器中。  
  
-   若要将备注和说明添加到模型元素，可以创建注释，然后将它们链接到元素。  
  
-   若要在关系图上整洁地对齐列或行形状，可以安装“对齐形状”命令。 这是可作为一个 UML 扩展示例： [UML： 对齐形状命令](http://code.msdn.microsoft.com/UML-command-to-Align-4139c0d7)  
  
### <a name="to-export-a-diagram-as-an-image"></a>若要将关系图导出为图像  
 有关详细信息，请参阅[将关系图导出为图像](../modeling/export-diagrams-as-images.md)。  
  
##  <a name="extensions"></a> 扩展 UML 设计器  
 可以将新功能添加到 UML 工具并按照自己的需求调整关系图表示法。 有关详细信息，请参阅[扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)。  
  
 有几个示例扩展可用。 可以只安装并使用，或者可将其源代码用作自己扩展的基础。 这些示例包括：  
  
|||  
|-|-|  
|[对齐形状](http://code.msdn.microsoft.com/UML-command-to-Align-4139c0d7)|有助于整理关系图的菜单命令。|  
|[链接到文档](http://code.msdn.microsoft.com/Link-UML-elements-to-0adbf5a8)|将任何 UML 元素链接到 Word 标题、PowerPoint 幻灯片、任何类型的文件、UML 关系图或其他 UML 元素。 可以通过拖动轻松地进行链接。 之后，可以双击该元素，以查看链接的项。 例如，可以将用例链接到 Word 规范或详细的活动图中，将操作链接到情节提要幻灯片。|  
|[快速输入](http://code.msdn.microsoft.com/UML-Rapid-Entry-using-Text-0813ad8a)|使用文本输入，快速创建模型。 对于捕获会议中的想法很有用。|  
|[根据构造型的颜色](http://code.msdn.microsoft.com/UML-Color-Classes-by-07de2b70)|根据构造型的颜色类。 可以轻松扩展代码，以适用于自己的构造型。|  
|[域建模](http://code.msdn.microsoft.com/UML-Domain-Modeling-6df6f7f4)|业务模型的方便默认值。 默认情况下，将显示不带箭头的关联，并且操作不会出现在类中。|  
  
## <a name="see-also"></a>请参阅  
 [创建 UML 建模项目和关系图](../modeling/create-uml-modeling-projects-and-diagrams.md)   
 [分析体系结构和建模](../modeling/analyze-and-model-your-architecture.md)   
 [为应用程序创建模型](../modeling/create-models-for-your-app.md)


