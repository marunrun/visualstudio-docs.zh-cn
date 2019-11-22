---
title: 'UML Sequence Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.sequencediagram.linktosequencediagram
- vs.teamarch.logicalclassdiagram.createlifeline
- vs.teamarch.componentdiagram.createlifeline
helpviewer_keywords:
- diagrams - modeling, sequence
- sequence diagrams
- UML diagrams, sequence
- interactions, UML
- diagrams - modeling, UML sequence
- UML interactions
- UML, sequence diagrams
- UML sequence diagrams
- behaviors, UML
ms.assetid: 5990ef7c-ba60-4e20-a36d-e29c1fa6c8bb
caps.latest.revision: 55
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8c5906084fc7db96ddf304e8362bf7692dac62d5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297150"
---
# <a name="uml-sequence-diagrams-guidelines"></a>UML Sequence Diagrams: Guidelines
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can draw a *sequence diagram* to show an interaction. 交互是类、组件、子系统或参与者的典型实例之间的消息序列。

 UML 序列图是 UML 模型的一部分，并且仅存在于 UML 建模项目中。 To create a UML sequence diagram, on the **Architecture** menu, click **New UML or Layer Diagram**. Find out more about [UML sequence diagram elements](../modeling/uml-sequence-diagrams-reference.md) or [UML modeling diagrams](../modeling/edit-uml-models-and-diagrams.md) in general. For a video demonstration, see [Sketching Interactions by using Sequence Diagrams (2010)](https://channel9.msdn.com/Blogs/clinted/UML-with-VS-2010-Part-7-Sketching-Interactions-with-Sequence-Diagrams).

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="in-this-topic"></a>在本主题中
 [Using UML Sequence Diagrams](#Using)

 [Basic Steps for Drawing Sequence Diagrams](#BasicSteps)

 [Creating and Using Simple Sequence Diagrams](#Simple)

 [Classes and Lifelines](#ClassesAndLifelines)

 [Creating Reusable Interaction Sequences](#Multiple)

 [Collapsing Groups of Lifelines](#Collapse)

 [Describing Control Structures with Fragments](#Fragments)

## <a name="Using"></a> Using UML Sequence Diagrams
 序列图可在不同的程序详细信息级别用于实现各种用途。 需要绘制序列图的典型情况如下所示：

- 如果拥有汇总了系统用户及其目标的用例图，则可以绘制序列图，用于描述系统的主要组件如何交互以实现每个用例的目标。 For more information, see [UML Use Case Diagrams: Guidelines](../modeling/uml-use-case-diagrams-guidelines.md).

- 如果已标识到达组件接口的消息，则可以绘制序列图，用于描述组件的内部部件如何交互以实现每个传入消息所需的结果。 For more information, see [UML Component Diagrams: Guidelines](../modeling/uml-component-diagrams-guidelines.md).

  绘制序列图有以下几个好处：

- 可以轻松了解任务在组件之间的分布方式。

- 可以识别使软件更新变得困难的交互模式。

## <a name="relationship-to-other-diagrams"></a>与其他关系图的关系
 可以通过多种方法组合使用 UML 序列图和其他关系图。

#### <a name="lifelines-and-types"></a>生命线和类型
 在序列图中绘制的生命线可以表示系统中的组件或类的典型实例。 可以根据类型创建生命线，也可以根据生命线创建类型，并且可以在 UML 类图和 UML 组件图中显示类型。 For more information, see [Classes and Lifelines](#ClassesAndLifelines).

#### <a name="parameter-types"></a>参数类型
 对于在生命线之间发送的消息中使用的参数类型和返回值，也可以在 UML 类图中进行描述。

#### <a name="use-case-details"></a>用例详细信息
 用例表示用户的目标以及实现该目标的步骤序列。 可以通过多种方法描述步骤序列。 一种方法是绘制显示用户与系统主要组件之间的交互的序列图。 For more information, see [UML Use Case Diagrams: Guidelines](../modeling/uml-use-case-diagrams-guidelines.md).

## <a name="BasicSteps"></a> Basic Steps for Drawing Sequence Diagrams
 For a complete list of elements on sequence diagrams, see [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md).

> [!NOTE]
> Detailed steps for how to create any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-create-a-sequence-diagram"></a>创建序列图

1. On the **Architecture** menu, click **New UML or Layer Diagram**.

2. Under **Templates**, click **UML Sequence Diagram**.

3. 命名该关系图。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a new modeling project**, and then click **OK**.

    A new sequence diagram appears with the **Sequence Diagram** toolbox. 该工具箱中包含所需的元素和连接线。

   ![Parts of a sequence diagram](../modeling/media/uml-sequence.png "UML_Sequence")

#### <a name="to-draw-a-sequence-diagram"></a>绘制序列图

1. Drag **Lifelines** (1) from the **Toolbox** onto the diagram to represent instances of classes, components, actors, or devices.

    > [!NOTE]
    > You can also create a lifeline by dragging an existing class, interface, actor or component from **UML Model Explorer** onto the diagram. 这将创建一个表示所选类型的实例的生命线。

2. 绘制消息，用于显示生命线如何协作以实现特定目标。

     要创建消息（3、4、6、7），请单击消息工具。 然后在希望消息开始的位置单击发送生命线，然后单击接收生命线。

     此时接收生命线上将显示执行发生 (5)。 执行发生表示实例执行方法的一段时间。 可以创建从执行发生开始的其他消息。

3. 要显示来自未知事件源 (9) 或传播给未知接收方 (10) 的消息，请绘制一个起始于或终止于关系图上的空白区域的异步消息。 These messages are called *found messages* (9) and *lost messages* (10).

    > [!NOTE]
    > To move a group of lifelines that have lost or found messages, follow these steps to select the lifelines before you move them: Draw a rectangle around those lifelines, or press and hold the **CTRL** key while you click each lifeline. If you use **Select All** or **CTRL**+**A** to select all lifelines, and then move them, any lost or found messages attached to these lifelines will not move. 如果出现这种情况，你可以单独移动这些消息。

4. 为相同组件或系统的每个主要消息绘制序列图。

#### <a name="to-change-the-order-of-messages"></a>更改消息的顺序

- 在消息的生命线中向上或向下拖动该消息。 可以将它拖动到其他消息上方，也可以将它拖入或拖出执行块。

     \- 或 -

- Click the message and use the **UP ARROW** and **DOWN ARROW** keys to adjust message positions. Use **SHIFT+UP ARROW** and **SHIFT+DOWN ARROW** to change the order of the messages.

#### <a name="to-move-or-copy-message-sequences-on-the-sequence-diagram"></a>在序列图上移动或复制消息序列

1. Right-click a message (3, 4) and then click **Copy**.

2. Right-click the execution occurrence (5) or a lifeline (1) from which you want the new message to be sent, and then click **Paste**. 新发送方可以位于其他关系图上（如果需要）。

     消息及其所有附属消息的副本将添加到执行发生或生命线的结尾。

    > [!NOTE]
    > 粘贴的消息始终在执行发生或生命线的结尾显示。 粘贴消息之后，可以将它向上拖动到更早的位置。

#### <a name="to-display-and-edit-the-signature-text-for-a-message"></a>显示和编辑消息的签名文本

- 必须将目标生命线绑定或映射到类型，以便让签名文本可见。 要完成此任务，请执行以下步骤之一：

  - Right-click the lifeline, and then choose **Create Class**.

     或

  - Select the lifeline, press **F4**, and then in the **Properties** window, set the **Type** property to an existing type or specify the name for a new type. Right-click the message label, and then choose **Create Operation**.

    此时消息标签下将显示签名文本。 现在可以编辑签名文本。 For more information, see [Classes and Lifelines](#ClassesAndLifelines).

#### <a name="to-improve-the-layout-of-a-sequence-diagram"></a>改进序列图的布局

- Right-click a blank part of the diagram, and then click **Rearrange Layout**.

- To undo the operation, click **Edit**, and then click **Undo**.

#### <a name="to-change-the-package-that-owns-the-interaction"></a>更改拥有交互的包

1. In **UML Model Explorer**, find the Interaction that the sequence diagram displays.

    > [!NOTE]
    > The interaction will not appear in **UML Model Explorer** until you add the first lifeline to the sequence diagram.

2. 将交互拖动到包中。

     \- 或 -

     Right-click the Interaction, and then click **Cut**. Right-click the Package, and then click **Paste**.

## <a name="Simple"></a> Creating and Using Simple Sequence Diagrams
 最简单且使用最广泛的序列图格式只包含生命线和消息。 使用此类关系图，你可以清晰地显示设计中各对象之间或系统及其用户之间的典型交互序列。 这通常足够帮助你讨论和沟通设计。

 下面是在绘制简单序列图时需要考虑的一些事项。

### <a name="types-of-message"></a>消息的类型
 可以使用三种工具创建消息。

- Use the **Synchronous** tool to describe an interaction in which the sender waits for the receiver to return a response (3).

     A **<\<return>>** arrow will be shown at the end of the execution occurrence. 它指示控制回到发送方。

- Use the **Asynchronous** tool to describe an interaction in which the sender can continue immediately without waiting for the receiver (4).

- Use the **Create** tool to describe an interaction in which the sender creates the receiver (8).

     创建消息应是接收方接收的第一个消息。

### <a name="annotating-the-interactions"></a>对交互进行批注
 To describe more detail about the sequence, you can place a **Comment** anywhere on the diagram.

 Using **Comment Links**, you can link a comment to lifelines, executions, interaction uses, and fragments.

> [!CAUTION]
> 如果想要将注释附加到序列中的特定位置，则需将它链接到执行发生、交互使用或片段。 请不要将注释链接到生命线，因为在这种情况下，注释不会保持附加在序列中的正确位置。

 使用注释可以：

- 注明已在序列中的关键位置实现的目标。 这有助于读者查看交互的目标。

- 描述整个序列的整体目标。 将注释附加到初始执行发生或不进行附加。 例如，“客户已从菜单中点菜并获得报价”。

- 描述每个生命线的职责。 将注释附加到生命线。 例如，“订单管理器收集客户的菜单选择”。

- 注明可能作为所示典型序列的替代项执行的异常或替代项。 例如，“客户可以选择跳过此序列的其余部分”。

  - 请考虑使用片段作为此类注释更为正式的替代项。 See [Describing Control Structures with Fragments](#Fragments)

## <a name="deciding-the-scope-of-the-diagram"></a>确定关系图的范围
 明确了解关系图要显示哪些内容非常重要。

#### <a name="initiating-event"></a>初始事件
 每个关系图都应显示从一个初始事件产生的交互序列。 例如，初始事件可能是：

- 用户启动一个用例，例如，打开网页订购午餐。

- 消息从一个系统组件传送到另一个系统组件，例如，查询客户想要购买的物品的可用性。

- 状态更改触发事件，例如，某个物品的库存低于阈值。

#### <a name="level-of-detail"></a>详细级别
 序列图可以显示不同的详细信息级别。 你可以几乎独立地在两个单独的维度中确定详细信息级别：

 生命线可以表示下列详细信息级别之一：

- 已经存在或将要开发的程序代码中的对象。

- 组件或其子组件，通常忽略外观、代理和其他连接机制。

- 系统和外部参与者

  消息可以表示下列详细信息级别之一：

- API 或 Web 接口的程序代码中的软件消息。

- 事务或子事务，例如，用户和系统之间或代码和数据库之间的事务或子事务。

- 用例 － 用户和系统之间的主要交互。

  无论是要浏览现有代码还是要描述新设计，绘制并讨论详细信息级别更低的视图通常很有用。

## <a name="describing-variations"></a>描述变体
 该关系图显示单个典型事件序列。 如果想要显示可能的替代项（例如失败方案），则可以使用以下两种选项之一：

- 绘制单独的序列图以描述这些方案

- Use [Describing Control Structures with Fragments](#Fragments) to show loops, alternatives, and so on.

## <a name="assessing-the-design"></a>评估设计
 可以使用该关系图评估任务在其对象或组件之间的分布情况。 如果看到下列模式，请考虑进行重构：

- 一个生命线似乎在执行所有操作，调用其他所有内容，而另一个生命线只是被动响应。

- 许多消息跨越生命线。 每个生命线应仅向邻近的几个生命线发送消息，不应与其邻近生命线的邻近生命线通信。 通常应该可以排列生命线，以便消息只在几个位置跨越生命线；在具有交点的位置，目标生命线还不应交换跨越了生命线的消息。

- 某些生命线似乎在处理多种类型的任务。 应该可以轻松找到描述每个生命线的职责的简洁句子，其中汇总了生命线响应其接收的每个消息时所做的工作。

## <a name="ClassesAndLifelines"></a> Classes and Lifelines
 序列图中的生命线显示类或组件接口的实例。 可以通过两种方法命名生命线：

|**For this purpose**|**Use this format**|
|--------------------------|-------------------------|
|类型的匿名实例。<br /><br /> 如果每个类型只有一个生命线，则使用这种格式。|*typeName*|
|类型的命名实例。<br /><br /> 如果想要显示涉及同一类型的多个实例的序列，则使用此格式。|*objectName*:*typeName*|

### <a name="creating-lifelines-from-types"></a>根据类型创建生命线
 例如，你可以根据已在类图中定义的类创建新生命线。

> [!NOTE]
> 执行此任务之前，请确保已拥有现有序列图。

##### <a name="to-create-a-lifeline-from-an-existing-type"></a>根据现有类型创建生命线

- 将类、组件或接口从 UML 模型资源管理器拖动到序列图中。

   \- 或 -

  1. Right-click the class, component, or interface on its respective diagram, and then click **Create Lifeline**.

  2. In the **Create Lifeline** dialog box, select a sequence diagram, and then click **OK**.

     此时将显示新的命名实例生命线，其类型为你拖动的类型。

  > [!NOTE]
  > 可以根据需要多次重复此操作。 这将创建具有不同实例名的生命线。

##### <a name="to-change-the-type-of-a-lifeline"></a>更改生命线的类型

1. Right-click a lifeline, and then click **Properties**.

2. In the **Properties** window, set the **Type** property. 可以从下拉菜单中选择一个类型，也可以键入新名称。

### <a name="creating-classes-from-lifelines"></a>根据生命线创建类
 如果已创建一个或多个序列图，则可以通过根据这些序列图创建类或接口来汇总生命线。

##### <a name="to-create-a-class-or-interface-from-a-lifeline"></a>根据生命线创建类或接口

1. Right-click the lifeline, and then click **Create Class** or **Create Interface**.

     此时 UML 模型资源管理器中将显示新类或新接口。

2. 在生命线接收到的每个消息的类或接口中创建操作：

    1. 选择想要包括的所有消息。

    2. Right-click one of the messages, and then click **Create Method**.

         新类或新接口具有每个选定消息的操作。

         The operation name appears below each message arrow, and in the **Operation** property of the message.

         如果消息包括“（参数 : 类型）”形式的参数，则它们将在新操作的参数列表中显示。

        > [!NOTE]
        > 如果要在序列图中添加新消息，则必须重复此步骤。

3. 要查看新类或新接口的详细信息，请将其添加到类图或组件图中。

    1. 打开或创建一个类图或组件图。

    2. Drag the new class or interface from **UML Model Explorer** to a class diagram.

         此时类图中将显示新类或新接口。

         \- 或 -

    3. Drag the new interface from **UML Model Explorer** onto a component or port in a component diagram.

         接口将在组件上显示为棒糖形。

### <a name="creating-classes-for-parameters"></a>创建参数的类
 可以在序列图上的消息中包括参数。 可以使用 UML 类图描述参数类型。

## <a name="Multiple"></a> Creating Reusable Interaction Sequences
 可以使用单独的关系图描述包含想要分离出去的或几个关系图共有的详细信息的序列。

 可以在一个关系图上创建指向另一个关系图中的详细信息的交互使用矩形 (12)。

 双击一个交互使用，打开链接到它的序列图。

#### <a name="to-create-a-reusable-interaction-sequence-from-existing-lifelines"></a>根据现有生命线创建可重用交互序列

1. In the **Toolbox**, click **Interaction Use**.

2. 在序列图上，按住鼠标按钮，拖过想要包括在可重用序列中的生命线。 从想要在其中插入交互使用的垂直位置开始。

     交互使用将在序列图上的选定生命线中显示。

3. 双击交互使用上的名称，将其重命名为描述此关系图中可重用序列效果的名称。

     \- 或 -

     使用参数编写类似函数调用的名称。

4. 将交互使用链接到另一个序列图。 右键单击交互使用，然后：

     Click **Create New Sequence** to create a new sequence diagram

     \- 或 -

     Click **Link to Sequence** to link to an existing diagram.

     Visual Studio 将在交互使用和新交互序列之间创建一个链接。

     此时解决方案中将显示新序列图。 它包含你用于创建交互使用的生命线。

    > [!NOTE]
    > 新关系图将只包括你用于创建交互使用的生命线。 新关系图将不包括在交互使用之后创建的生命线，即使交互使用现在覆盖这些生命线。

#### <a name="to-create-a-reusable-sequence-from-existing-messages"></a>根据现有消息创建可重用序列

- Right-click the message that you want to move, and then click **Move to Diagram**.

  Visual Studio：

  - 用交互使用替换选定消息及任何附属消息。

  - 将替换的消息移动到新序列图。

  - 在交互使用和新序列图之间创建一个链接。

#### <a name="to-navigate-to-the-sequence-referenced-by-an-interaction-use"></a>导航到交互使用引用的序列

- 双击交互使用。

     \- 或 -

     Right-click the interaction use and then click **Go to Sequence**.

### <a name="creating-a-placeholder-with-an-interaction-use"></a>使用交互使用创建占位符
 可以创建交互使用而不将其链接到另一个关系图。 You can use this as a placeholder for a part of the sequence whose details are yet to be worked out. Use the name of the interaction use to indicate the outcome that you want.

## <a name="Collapse"></a> Collapsing Groups of Lifelines
 可以将一组生命线折叠到一起，以便该组显示为一个生命线。 这有助于你将一组对象可视化为单个组件。 折叠组中的生命线之间的消息和交互使用处于隐藏状态。 包括其他生命线的消息和交互序列处于显示状态。

#### <a name="to-collapse-a-group-of-lifelines-together"></a>将一组生命线折叠到一起

1. 选择两个或多个生命线。

2. Right-click one of them, and then click **Collapse**.

     这些单独的生命线将替换为一个生命线。

     仅涉及组成员的消息和交互使用处于隐藏状态。

3. 要重命名组，请单击名称。

    > [!NOTE]
    > 展开组时，组名将丢失。

#### <a name="to-expand-a-collapsed-group"></a>展开折叠的组

- Right-click the collapsed lifeline, and then click **Expand**.

    > [!NOTE]
    > 组的名称以及从该组到注释或工作项的任何链接都将丢失。

## <a name="Fragments"></a> Describing Control Structures with Fragments
 可以使用组合片段 (13) 定义序列图中的循环、分支和并发处理。 或者，可以考虑改用活动图。 活动图在显示参与者之间的消息时不太有用，但某些情况下，在显示循环、分支和并发时比较有用。

 For a full list of the types of fragment, see [Describe control flow with fragments on UML sequence diagrams](../modeling/describe-control-flow-with-fragments-on-uml-sequence-diagrams.md).

#### <a name="to-create-a-combined-fragment"></a>若要创建组合片段

1. 选择一个消息，或消息序列（其中所有消息都在同一执行发生或生命线上开始）。

    > [!NOTE]
    > 选择消息箭头，而不要选择消息指向的执行发生。

2. Right-click one of the messages, point to **Surround With**, and then click the type of fragment that you require.

     此时将显示新片段。 它包含你选择的消息。

     如果组合片段类型允许多个片段，则也将显示空片段。

3. To set the guard of a fragment, right-click the fragment border, and then click **Properties**. Set the **Guard** property.

     临界用于定义分支或循环的条件。

4. To add a new fragment to a kind that allows multiple fragments, right-click the boundary of a fragment, and point to **Add**. Click either **Interaction Operand Before** or **Interaction Operand After**.

5. 要将新消息添加到片段中，请使用消息工具，或者使用复制和粘贴。

## <a name="see-also"></a>请参阅
 [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md) [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [Video: Sketching Interactions by using Sequence Diagrams](https://go.microsoft.com/fwlink/?LinkId=201113)
