---
title: Edit UML models and diagrams | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 00ac30cc7e9ee3aff0dd64f015a4b4954972c09a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295534"
---
# <a name="edit-uml-models-and-diagrams"></a>编辑 UML 模型和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过由多种不同类型的关系图提供的视图创建和编辑 UML 模型。 通过在你的系统上提供不同的透视图，这些关系图有助于了解和讨论设计和需求的不同方面。 Visual Studio 提供了五种最常用的 UML 关系图模板。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 本主题介绍了用于编辑在不同的关系图类型之中共有的模型的方法。 For more information that is specific to particular types of diagrams, see [Create models for your app](../modeling/create-models-for-your-app.md).

## <a name="in-this-topic"></a>本主题内容

- [UML Diagrams are Views of a UML Model](#Views)

- [Creating UML Modeling Diagrams](#Creating)

- [Drawing UML Modeling Diagrams](#Drawing)

- [Editing Shapes and Connectors](#Editing)

- [Undoing Changes to the Model](#Undo)

- [Sharing Elements between Diagrams](#Sharing)

- [Copying Elements and Groups of Related Elements](#Copying)

- [Deleting a Model Element or its Views](#Deleting)

- [Searching text in a diagram](#Searching)

- [Preparing a Diagram for Presentation](#presentation)

- [Extending the UML Designers](#extensions)

## <a name="Views"></a> UML Diagrams are Views of a UML Model
 只能在建模项目中创建和使用 UML 关系图。 For more information about how to create diagrams and projects, see [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md).

- 一个建模项目只包含一个 UML 模型。 项目中的每个 UML 关系图都是 UML 模型视图。

- You can see the model in **UML Model Explorer**. On the **Architecture** menu, point to **Windows**, and then click **UML Model Explorer**.

- 关系图上的每个形状都是模型中元素的视图。 当将新形状置于关系图上时，将在模型中创建一个新元素。

- When you save any diagram, Visual Studio saves the whole model, all its diagrams, and the modeling project file.

## <a name="Creating"></a> Creating UML Modeling Diagrams

1. On the **Architecture** menu in Visual Studio, click **New UML or Layer Diagram**.

2. 选择并命名关系图。

3. In **Add to modeling project**, select an existing modeling project, or select **Create a new modeling project**.

   > [!NOTE]
   > 建模关系图必须存在于建模项目内。

   还可以向解决方案资源管理器中的一个现有的建模项目添加关系图。 Right-click the modeling project, point to **Add**, and then click **New Item**.

#### <a name="to-create-an-empty-uml-modeling-project"></a>若要创建空的 UML 建模项目

- On the **File** menu, point to **New**, click **Project**, and in the **New Project** dialog box, double-click **Modeling Projects**.

  For more information about how to manage modeling projects, see [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md).

## <a name="Drawing"></a> Drawing UML Modeling Diagrams
 建模图显示通过关系链接的模型元素集合。 每个元素显示为一个形状，每个关系显示为两个形状之间的连接线。

 有两种类型的工具，一种用于元素，另一种用于关系。 For example, in the UML class diagram Toolbox, **Class** is an element tool, and **Association** is a relationship tool.

> [!NOTE]
> If you want information that is specific to particular diagram types, see [Create models for your app](../modeling/create-models-for-your-app.md).

#### <a name="to-create-elements-and-relationships-in-a-uml-modeling-diagram"></a>若要在 UML 建模关系图中创建元素和关系

1. 若要创建模型元素，则单击“工具箱”中的元素工具，然后单击希望元素在其中进行显示的关系图。 创建该元素后，通过拖动其句柄调整其大小和形状。

    在某些情况下，可以将新元素放置在另一个元素内。 例如，在 UML 类关系图上，可以将类放置在包内。

   > [!NOTE]
   > If you cannot see the toolbox, click **Toolbox** on the **View** menu.

2. 若要创建关系，则单击关系工具，单击想要关系从其开始的元素，然后单击想要关系以其结束的元素。

    不同类型的关系可以在不同类型的元素上启动或结束。 例如，在 UML 类关系图中，关联关系不能在 Comment 元素上开始或结束。

   > [!NOTE]
   > 若要多次使用同一个工具，请双击该工具。 When you have finished, click the **Pointer** tool.

   在某些类型的关系图上，还可以绘制简单的形状。 这些形状不是模型的一部分，但你可以使用它们强调部分关系图或将其分成不同的区域。

## <a name="Editing"></a> Editing Shapes and Connectors
 当调整形状大小或给形状涂色，或者重新布局连接线时，对基础模型没有任何影响。 但是，当重命名关系图上或 UML 模型资源管理器中的形状时，将在 UML 模型资源管理器中和显示该元素的任何其他关系图中重命名相应的元素。

> [!NOTE]
> 有一种创建新工具箱项的简单方法，你可以在新工具箱项中使用自选属性创建元素组或元素。 For more information, see [Define a custom modeling toolbox item](../modeling/define-a-custom-modeling-toolbox-item.md).

 下图显示了如何更改形状的大小或其名称。

 ![Adjusting a model element](../modeling/media/uml-drawadjust1.png "UML_DrawAdjust1")

> [!TIP]
> 内置命令不包括用于准确对齐形状的命名。 However, you can easily create your own alignment command by copying the code in the example in [Display a UML model on diagrams](../modeling/display-a-uml-model-on-diagrams.md).

 下图显示了如何调整连接线及其标签的布局和位置。

 ![Adjusting a connector](../modeling/media/uml-drawadjust2.png "UML_DrawAdjust2")

#### <a name="to-move-one-end-of-a-connector-to-another-shape"></a>若要将连接线的一端移动到另一个形状

1. 执行以下操作之一：

   - Press **CTRL** and move the end.

     \- 或 -

   - Right-click the connector and then click **Reconnect**.

2. 单击想要移动的连接线的一端。

3. 单击想要将连接线移动到其中的形状。

#### <a name="to-change-color-or-other-properties-of-an-element-relationship-or-diagram"></a>若要更改元素、关系或关系图的颜色或其他属性

- Click the element and set the fields in the **Properties** window.

     If you cannot see the **Properties** window, right-click the element, and then click **Properties.**

#### <a name="to-zoom-in-and-out-on-a-modeling-diagram"></a>若要在建模图上放大和缩小

- Press and hold the **CTRL** key while you rotate the mouse wheel.

     \- 或 -

- Press and hold **CTRL+SHIFT**, and then click the left or right mouse button.

     \- 或 -

- On the **Architecture Designers** toolbar, click the plus sign ( **+** ) or minus sign ( **-** ), or choose a zoom level.

## <a name="Searching"></a> Searching in a Diagram
 “快速查找”功能将查找关系图上的项。 You must set **Look in:** to **Current Document**.

#### <a name="to-search-for-text-in-a-modeling-diagram"></a>若要在建模图中搜索文本

1. Press **CTRL+F**.

     \- 或 -

     On the **Edit** menu, point to **Find and Replace**, and then click **Quick Find**.

    > [!NOTE]
    > In the **Find and Replace** dialog box, you must leave the **Look in** field set to **Current Document**. 不支持其他选项。

2. Type the text that you want to find, and then click **Find Next**.

    > [!NOTE]
    > 如果想要查找的文本位于折叠形状内，则将突出显示该形状。 Expand the shape, and then click **Find Next** again.

## <a name="Undo"></a> Undoing Changes to the Model
 You can undo and redo changes that you have made to the model and diagrams by using the **Undo** and **Redo** commands on the **Edit** menu.

 **Each modeling project has a single stack of changes.** 对模型和关系图所做的所有更改都保留在此堆栈中。 此堆栈还包括焦点从一个关系图移动到另一个关系图的更改。 “撤消”命令可反转此堆栈上的更改。

 例如，假设你执行了这些操作：对关系图 1 进行了更改；将焦点更改到关系图 2；更改了关系图 2。 撤消更改时，第一个撤销将反转最后一个更改；第二个撤消会将焦点移回到关系图 1；第三个撤消将反转对关系图 1 所做的更改。

 **Closing a diagram truncates the stack of changes.** 如果关闭关系图，则不能撤消在该关系图中执行的更改，并且不能撤消对模型或其任意关系图所做的早期更改。

 **You cannot undo while you are editing a property.** 当正在“属性”窗口或关系图上的标签中编辑属性时，仅可以撤消在该属性中所做的更改。 通过按 ENTER 键完成在属性中的更改，或按 ESC 键取消。 然后，你便可以在模型和关系图中撤消更改。

 **Closing a diagram without saving might not have the effect you expect.** 如果进行一些更改，然后关闭但没有进行保存，则所做的更改仍会保留在模型中。 如果想要关闭但不对其进行保存，则建议关闭整个模型。

## <a name="Sharing"></a> Sharing Elements between Diagrams
 可以将关系图中出现不止一次的模型元素作为特定实例。 这适用于类、接口、组件、用例和参与者。

 如果想要在不同的关系图中显示不同组的关系，这很有用。 例如，在一个关系图中，可以显示“客户”和“地址”类之间的关联。 在另一个关系图中，可以再次显示“地址”类及其相关的邮政区域。

 通过在任何关系图上选择模型元素的任何视图，或者在 UML 模型资源管理器中选择它，可以更改此模型元素的属性（例如，模型名称）。

 每种关系图只能显示几种模型元素。 例如，不能在组件图上显示用例。 因此，以下过程仅适用于模型元素和关系图的某些组合。

#### <a name="to-add-a-new-view-of-a-model-element-by-using-uml-model-explorer"></a>若要通过使用 UML 模型资源管理器，添加模型元素的新视图

1. To open **UML Model Explorer**, on the **Architecture** menu, point to **Windows**, and then click **UML Model Explorer**.

2. Drag the model element from **UML Model Explorer** to a compatible diagram in the same project.

     将显示提供模型元素的视图的形状，这可能不包括其他关系图或同一个关系图上的视图。

    > [!NOTE]
    > 将类或组件拖动到序列图上时，作用是不同的。 在这种情况下，将创建一个新的生命线，其类型为该类或组件。 For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

#### <a name="to-add-a-new-view-of-a-model-element-by-using-paste-reference"></a>若要使用“粘贴引用”添加模型元素的新视图

1. Right-click an existing element, and then click **Copy**.

    - 可以同时复制多个元素。 Hold down the CTRL key while you click each element, right-click one of them, and then click **Copy**.

2. Right-click an empty part of a compatible diagram, and then click **Paste Reference**.

     将显示同一元素的另一个视图。

    > [!NOTE]
    > This differs from the **Paste** command, which creates a new element in the model. For more information, see [Copying Elements and Groups of Related Elements](#Copying).

> [!NOTE]
> 如果添加到已通过关系连接的两个模型元素的关系图视图，则此关系的视图也会出现在关系图中。 只能通过从关系图删除其中一个元素或通过从模型中删除关系，来删除此视图。

## <a name="Copying"></a> Copying Elements and Groups of Related Elements
 可以复制并粘贴模型元素，并且可以复制和粘贴元素组及其之间的关系。

> [!NOTE]
> The **Paste** and **Paste Reference** commands have different effects. **Paste** creates new elements whose properties are like those of the copied elements. **Paste Reference** creates new views of the same elements.

#### <a name="to-copy-elements-and-their-relationships"></a>若要复制的元素和它们之间的关系

1. 在具有想要复制的元素的关系表中，选择一个或多个元素。

    > [!NOTE]
    > 不能复制关系，除非作为组元素的一部分。

2. On the **Edit** menu, click **Copy**.

3. 如果想要将元素复制到另一个关系图，则创建新关系图，或打开现有的关系图。

4. On the **Edit** menu, click **Paste**.

    - 将显示元素的副本，以及任何在它们之间进行链接的关系的副本。

    - 每个新元素将具有一个自动生成的新名称。

5. 调整新元素和关系的位置、名称和其他属性。

> [!NOTE]
> 不能将模型元素从一个模型复制到另一个模型，例如，在同一解决方案中有两个模型的情况下。 但是，可以将元素从一个关系图复制到另一个关系图。

#### <a name="to-copy-an-entire-diagram"></a>若要复制整个关系图

1. 创建新关系图。

2. 选择现有关系图中的所有元素，复制它们，然后将其粘贴到新的关系图中。

   不能通过在解决方案资源管理器中复制和粘贴，来复制关系图。

## <a name="Deleting"></a> Deleting a Model Element or its Views
 可以从关系图中删除某些类型的元素（尤其是分类器），而无需从模型中进行删除。 分类器是在类图中、组件图中和用例图中显示的主要元素。 它们可以显示在多个关系图上。 For these types of elements, there are two separate commands: **Remove from Diagram** and **Delete from Model**.

 与此相反，当从关系图中删除关系时，将始终从模型中删除。

> [!NOTE]
> UML 关系图上某些类型的元素具有标签。 通过在它们周围绘制矩形来选择此类元素时，可以选择标签，而不是拥有这些标签的元素。 不支持删除以这种方式选择的元素的子集。 To select a subset of these elements, press and hold the **CTRL** key while you click each element.

#### <a name="to-remove-a-classifiers-view-from-a-diagram"></a>若要从关系图删除分类器的视图

- Right-click the element on the diagram, and then click **Remove from Diagram**.

  \- 或 -

- Click the element on the diagram and then press the **DELETE** key.

  - 元素的此视图将会消失。 However, the element remains in the model, and you can still find it in **UML Model Explorer**. 任何相同元素的其他视图也将保留。

  - 终止于此形状的每个连接线将从关系图中删除，但其代表的关系将保留在模型中。 You can see the relationship in **UML Model Explorer** under **Relationships**, under each element that it connects.

#### <a name="to-delete-an-element-from-the-model"></a>若要从模型中删除元素

- Right-click the element either in **UML Model Explorer** or on a diagram, and then click **Delete from Model**.

  - 该元素将从显示它的每个关系图中删除。

  - 终止于此元素的每个关系也将从模型中删除。

#### <a name="to-delete-a-relationship-from-the-model"></a>若要从模型中删除关系

- Right-click the relationship on a diagram or in **UML Model Explorer**, and then click **Delete from Model**.

    > [!CAUTION]
    > 在没有将关系从模型中删除的情况下，则不能从关系图中删除该关系。

     该关系将从模型中删除，并且将从显示它的每个关系图中删除。

## <a name="presentation"></a> Preparing a Diagram for Presentation
 以下功能有助于强调关系图的特定部分、添加说明或将关系图划分为不同感兴趣的区域。

- 可以将关系图的任何部分复制到 Word、PowerPoint 或其他文档中。 Select the shapes and connectors you want, right-click and then click **Copy**.

- 可以更改任何形状或连接线的颜色。 Select one or more shapes and change the **Color** property. 如果看不到“属性”窗口，请按“F4”。

- On diagrams of some kinds, you can draw lines, rectangles and ellipses from the **Simple Shapes** section of the Toolbox. 这些形状并不构成 UML 模型的一部分。

- To label an area, you can drag a Comment from the Toolbox and then set its **Transparent** property to **True**. 就像“简单形状”一样，注释不构成 UML 模型的一部分，并且不会显示在 UML 模型资源管理器中。

- 若要将备注和说明添加到模型元素，可以创建注释，然后将它们链接到元素。

### <a name="to-export-a-diagram-as-an-image"></a>若要将关系图导出为图像
 For more information, see [Export diagrams as images](../modeling/export-diagrams-as-images.md).

## <a name="extensions"></a> Extending the UML Designers
 可以将新功能添加到 UML 工具并按照自己的需求调整关系图表示法。 For more information, see [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md).

## <a name="see-also"></a>请参阅
 [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md) [Analyzing and Modeling Architecture](../modeling/analyze-and-model-your-architecture.md) [Create models for your app](../modeling/create-models-for-your-app.md)
