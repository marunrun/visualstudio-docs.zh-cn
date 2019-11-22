---
title: 'UML Activity Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML diagrams, activity
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- activity diagrams
- UML, activity diagrams
ms.assetid: fe5dbe96-79ab-483a-b9bc-44d0d1d3efc2
caps.latest.revision: 50
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 692859008891439e4af3d751306bfd3ee6d351e8
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298995"
---
# <a name="uml-activity-diagrams-guidelines"></a>UML 活动图：准则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可以绘制活动图以按照由一系列操作构成的工作流的形式描述业务流程或软件算法。 用户、软件组件或设备可以执行这些操作。 For a video demonstration, see: [Capture Business Workflows by using Activity Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-4-capture-business-workflows).

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 To create a UML activity diagram, on the **Architecture** menu, click **New UML or Layer Diagram**.

 可将活动图用于多种目的：

- 描述用户与你的系统之间的业务流程或工作流。 For more information, see [Model user requirements](../modeling/model-user-requirements.md).

- 描述某一用例中执行的步骤。 For more information, see [UML Use Case Diagrams: Guidelines](../modeling/uml-use-case-diagrams-guidelines.md).

- 描述软件中的方法、函数或操作。 For more information, see [Model your app's architecture](../modeling/model-your-app-s-architecture.md).

  绘制活动图可以帮助你改进流程。 如果现有流程图经证实是非常复杂的，可以考虑如何简化这一流程。

  For reference information about the elements on activity diagrams, see [UML Activity Diagrams: Reference](../modeling/uml-activity-diagrams-reference.md).

## <a name="Relationships"></a> Relationship to Other Diagrams
 如果绘制活动图来描述业务流程或用户使用系统的方式，则可以绘制用例图来显示相同信息的不同视图。 在用例图中，将操作绘制为用例。 为用例指定与对应的操作相同的名称。 用例视图可以为你带来以下好处：

- 使用“包括”关系在一个关系图中显示较大操作/用例如何由较小操作/用例组成。

- 将每个操作/用例显式连接到其执行过程中涉及的用户或外部系统。

- 绘制由你的系统或系统的每个主要组件支持的操作/用例周围的边界。

  还可以绘制活动图来描述软件操作的详细设计。

  在活动图中，可以显示操作之间传递的数据流。 See the section on [Describing Data Flow](#DataFlows). 但是，活动图不描述数据的结构。 为实现此目的，你可以绘制一个 UML 类图。 For information see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).

## <a name="BasicSteps"></a> Basic Steps for Drawing Activity Diagrams
 Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-draw-an-activity-diagram"></a>绘制活动图

1. On the **Architecture** menu, click **New UML or Layer Diagram**.

2. Under **Templates**, click **UML Activity Diagram**.

3. 命名该关系图。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**.

#### <a name="to-draw-elements-on-an-activity-diagram"></a>在活动图上绘制元素

1. 将元素从工具箱中拖动到关系图上。

     首先将主要活动放置在关系图上，再将这些活动连接起来，然后添加最终的润饰（如初始节点和最终节点）。

    > [!NOTE]
    > 不能将现有元素从 UML 模型资源管理器拖动到关系图上。

2. 若要连接这些元素，请按以下步骤进行操作：

    1. In the **Activity Diagram** toolbox, click **Connector**.

    2. 在关系图上，单击源元素。

    3. 单击目标元素。

        > [!NOTE]
        > 若要多次使用某个工具，请在工具箱中双击该工具。

#### <a name="to-move-an-activity-to-another-package"></a>将一个活动移动到另一个包

- In **UML Model Explorer**, drag the activity into a package.

     \- 或 -

- In **UML Model Explorer**, right-click the activity and click **Cut**. Then right-click the package and click **Paste**.

    > [!NOTE]
    > 该活动仅在你将第一个元素添加到关系图中时显示在 UML 模型资源管理器中。

## <a name="SimpleControlFlow"></a> Describing Control Flow
 活动图以一系列操作的形式描述业务流程或软件算法。 连接器箭头显示控制如何按顺序从一个操作传递到下一个。 通常，一个操作只能在其前一个操作完成后开始。

 下图是一个示例，它描述如何使用操作、连接线、分支和循环演示一系列操作。 以下各节将更详细地描述每个元素。

 ![A simple activity diagram](../modeling/media/uml-actguidectrl.png "UML_ActGuideCtrl")

 Activity diagrams use **Actions** and **Connectors** to describe your system or application as a series of actions with the control flowing sequentially from one action to the next.

- Create an **Action** (1) for each major task that is performed by a user, the system, or both in collaboration.

  > [!NOTE]
  > 尝试只使用少量操作来描述流程或算法。 You can use **Call Behavior Actions** to define each action in more detail in a separate diagram, as described in [Describing Sub-activities with Call Behavior Actions](#Subactivities).

- 确保每个操作的标题都清楚地表明操作的典型用途。

- Link the actions in sequence with **Connectors** (2).

- 每个操作都将在控制流中的下一个操作开始之前结束。 If you want to describe actions that overlap, use a **Fork Node** as described in the section [Concurrent Flows](#Concurrent).

  虽然该关系图描述了操作序列，但它不描述操作的执行方法（即，将控制从一个操作传递到下一个操作的方式）。 如果使用该关系图来表示业务流程，则可能会传递控制，例如当一个人向他人发送电子邮件时。 如果使用该关系图来表示软件设计，则可能会通过从一个语句到下一个语句的常规执行流来传递控制。

### <a name="describing-decisions-and-loops"></a>描述决策和循环

- Use a **Decision Node** (3) to indicate a point where the outcome of a decision dictates the next step. 可以绘制所需数目的传出路径。

- 如果使用活动图来定义应用程序的一部分，则应定义临界条件 (4)，从而清楚地知道何时应采用每条路径。 Right-click the connector, click **Properties**, and in the **Properties** window, type a value for the **Guard** field.

- 并不总是需要定义临界条件。 例如，如果使用活动图来描述业务流程或交互协议，则分支会定义可供用户或交互组件使用的选项范围。

- Use a **Merge Node** (5) to bring together two or more alternative flows that branched at a **Decision Node**.

    > [!NOTE]
    > You should use a **Merge Node** to bring together alternative flows, instead of bringing the flows together at an action. In the example, it would not be correct to connect from the decision node directly back to **Choose Menu Item**. 这是因为操作在控制线程到达其所有传入连接线之前不会开始。 因此，只应在一个操作中组合并发流。 For more information, see [Concurrent Flows](#Concurrent).

- 使用分支来描述循环，如示例中所示。

    > [!NOTE]
    > 像在程序代码中一样，尝试按照结构完整的方式嵌套循环。 如果描述的是现有业务流程，这样做可能会带来一些改进流程的机会。

### <a name="starting-the-activity"></a>启动活动
 可以通过两种方式指示活动的入口点：

- **Initial Node**

     Create one **Initial Node** (6) to indicate the first action of the activity.

     在描述子活动时或在无需显式声明启动活动的对象时，此方法最有用。 例如，活动“订餐”很明显会在顾客饥饿时启动。

- **Accept Event Node**

     Create **Accept Event Nodes**, as described in the section [Concurrent Flows](#Concurrent), to indicate the start of a thread that responds to a particular event, such as a user input. 不要提供节点的传入流。 忽略传入流指示线程将在每次发生相应事件时启动。

     在描述对某个特定外部事件的响应时，此方法非常有用。

### <a name="ending-the-activity"></a>结束活动
 Use an **Activity Final Node** (7) to indicate the end of an activity.

- When a thread of control reaches an **Activity Final Node**, all the activity's concurrent actions and sub-activities terminate.

- 可以使用多个活动最终节点来减少其他连接线的混乱程度。

### <a name="interrupting-the-activity"></a>中断活动
 若要描述如何中断活动的普通流（例如，如果用户决定取消流程），可以创建一个用于侦听该事件的接受事件节点。 For more information, see the section [Concurrent Flows](#Concurrent). 创建从一个节点到活动最终节点 (7) 的控制流。

### <a name="swimlanes"></a>泳道
 有时，将活动的多个操作安排到与执行这些操作的各个对象或业务角色相对应的区域中会很有用。 These areas are conventionally arranged in columns and are called *swimlanes*.

- Use lines or rectangles from the **Simple Shapes** section of the Toolbox to draw swimlanes or other areas.

- To label each swimlane, create a comment and set its **Transparent** property to **True**.

  简单形状不构成 UML 模型的一部分，并且不出现在 UML 模型资源管理器中。

## <a name="DataFlows"></a> Describing Data Flow
 可以使用以下两种方式之一描述传入和传出活动的数据：

- Use an **Object Node**. 这是描述活动之间的信息流动的最简单方法。 对象节点类似于程序中的变量。 它表示用于存储从一个操作传递到另一个操作的一个或多个值的项。

- Use an **Output Pin** and an **Input Pin**. 利用此方法，可以分别描述来自一个操作的输出和到另一个操作的输入。 插针类似于程序中的参数。 插针表示对象可通过其进入和离开一个操作的端口。

    > [!NOTE]
    > For an overview of the elements used in this section, see the Data Flows section of the topic see [UML Activity Diagrams: Reference](../modeling/uml-activity-diagrams-reference.md).

### <a name="describing-data-flow-with-object-nodes"></a>使用对象节点描述数据流
 大多数控制流都会传输数据。 例如，来自“客户提供详细信息”操作的输出流会传输对送货地址的引用。

 若要在关系图中描述此数据，可以将一条连接线替换为一个对象节点和两条连接线，如下图所示。

 ![Object nodes can show data passed between actions](../modeling/media/uml-actguidedata.png "UML_ActGuideData")

 请注意圆角矩形（例如“调度货物”）表示正在处理的操作。 方角矩形（如“送货地址”）表示从一个操作到另一个操作的对象流。

 为对象节点指定一个名称，此名称反映作为在操作之间流动的对象的管道或缓冲区的节点角色。

 You can set the **Type** of the object node in the Properties window. 类型可以是基元类型（如整型）或已在类图中定义的类、接口或枚举。 例如，你可以创建一个 Shipment Address 类，该类具有 Street Address、City 等特性以及与另一个名为 Customer 的类的关联。 For more information, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).

> [!NOTE]
> If you type the name of a type that has not yet been defined, an item will be added under **Unspecified Types** in UML Model Explorer. 如果随后在类图中定义该名称的类型，则应重置对象节点的类型，以使其引用新的类型。

#### <a name="buffering-data-in-object-nodes"></a>在对象节点中对数据进行缓冲
 一个对象节点可用作多个对象的缓冲区。 在下图中，控制流显示用户可以多次访问“[选择更多]”循环 (1)，同时“已点的菜”对象节点 (2) 会累积用户的选择。 最后，当用户完成选择时，控制会传递到“确认订单”操作 (3)，该操作接受“已点的菜”缓冲区中的完整的选项列表。

 ![Buffering data in object nodes](../modeling/media/uml-actguidebuffer.png "UML_ActGuideBuffer")

 通过设置对象节点的属性，可以指定各个项在缓冲区中的存储方式：

- Set the **Ordering** property:

  - **Unordered** to specify a random or unspecified order. （默认。）

  - **Ordered** to specify an order according to a specific key.

  - **Fifo** to specify an order of first-in, first-out.

  - **Lifo** to specify an order of last-in, first-out.

- Set the **Upper Bound** property to specify the maximum number of objects that can be contained in the buffer. 默认值为 *。 这表示不存在任何限制。

### <a name="describing-data-flow-with-input-and-output-pins"></a>使用输入和输出插针描述数据流
 Use an **Output Pin** and an **Input Pin** to separately describe the outputs from one action and the inputs to another.

 ![Input and output pins are action parameters](../modeling/media/uml-actguidepins.png "UML_ActGuidePins")

 To create a pin, click **Input Pin** or **Output Pin** on the toolbox and then click an action. 然后，可以围绕此操作的周边移动插针，并更改其名称。 You can create input and output pins on any kind of action, including **Call Behavior Actions**, **Call Operation Actions**, **Send Signal Actions**, and **Accept Event Actions**.

 两个插针之间的连接线表示一个对象流，如同流入和流出对象节点的流一样。

 为每个插针指定一个名称，该名称指示插针生成或接受的对象的角色，如参数名称。

 You can set the type of objects transmitted in the **Type** property. 这必须是已在 UML 类图中创建的类型。

 已连接的插针之间的对象流必须在某些方面是兼容的。 这可能是因为输出插针所生成的对象属于输入插针的类型的派生类型。

 或者，可以指定对象流包括一个转换，以在输出插针的类型和输入插针的类型之间进行数据转换。 最常见的此类转换是从更大的类型中提取适当的部分。 图中的示例暗含从“订单详细信息”中提取“送货地址”的转换。

## <a name="Details"></a> Defining an Action in More Detail
 除了通过操作名称来明确指明操作通常应实现的结果之外，还可以通过以下方式为操作添加更多详细信息：

- Write a more detailed description in the **Body** property. 例如，可以编写程序代码或伪代码的片段，或编写所实现的结果的完整说明。

- 将操作替换为调用行为的操作，并在单独的活动图中描述其详细行为。 See [Describing Sub-activities with Call Behavior Actions](#Subactivities).

- Set the action's **Local Postconditions** and **Local Preconditions** properties to describe its outcome in more specific detail. For more information, see [Defining Postconditions and Preconditions](#Postcondition).

### <a name="Subactivities"></a> Describing Sub-activities with Call Behavior Actions
 可以使用单独的活动图来描述操作的详细行为。 被调用行为是一个活动图，它在主活动图中由调用行为的操作表示。 还可以使用调用行为的操作来描述在不同的活动之间共享的行为，从而无需多次绘制子活动。

 在下图中，关系图 1 显示具有调用行为的操作的活动；关系图 2 显示一个子活动图，其中显示了被调用行为。

 ![A separate activity diagram shows detailed actions](../modeling/media/uml-actguidedetail.png "UML_ActGuideDetail")

##### <a name="to-describe-a-sub-activity-with-a-call-behavior-action"></a>使用调用行为的操作描述子活动

1. To create the diagram for the sub-activity, in **Solution Explorer**, right-click your modeling project, point to **Add**, and then click **New Item**.

2. In the **Add New Item** dialog box, under **Templates** click **Activity Diagram** and in the **Name** box type the name that you plan to give your **Call Behavior Action**.

3. 为子活动绘制详细的工作流。 这是被调用的行为。

    - In the called sub-activity diagram, the **Initial Node** indicates where control starts when the called behavior is invoked. The **Activity Final Node** shows where control should return to the parent activity.

4. Set the **Behavior** property of the **Call Behavior Action** to refer to the called behavior diagram.

    > [!NOTE]
    > The sub-activity diagram must have some elements on it or the diagram will not be available in the drop-down list for the **Behavior** property. Also, the trident icon will not appear on your **Call Behavior Action** shape until you set its **Behavior** property.

5. Set the **Is Synchronous** property of the action to indicate whether your activity waits for the called activity to complete.

    - If you set **Is Synchronous** to false, you are indicating that the flow can continue to the next action before the called activity finishes. 不应在操作中定义输出插针或传出数据流。

### <a name="describing-data-flow-in-and-out-of-sub-activities"></a>描述流入和流出子活动的数据流
 可以按照在软件中使用参数的方式来描述流入和流出子活动的数据流。

- 在被调用行为的操作中为流入或流出操作的每段数据创建输入插针和输出插针 (1)。 为每个插针指定适当的名称。

- In the sub-activity diagram, create an **Activity Parameter Node** (2) for each input and output pin on the calling action. 为每个节点指定与其所对应的插针相同的名称。

  > [!NOTE]
  > 活动参数节点类似于对象节点。 To check what type of node that you are looking at, right-click the node and then click **Properties**. 节点类型显示在“属性”窗口的标题中。

- 在子活动图中绘制连接线，这些连接线将显示流入或流出每个活动参数节点的对象流。

  ![Pins on Call Behavior map to activity parameters](../modeling/media/uml-actguidesub.png "UML_ActGuideSub")

### <a name="Postcondition"></a> Defining Postconditions and Preconditions
 You can use the **Local Postconditions** and **Local Preconditions** properties to specify in detail the outcome of an action. 这些属性描述操作的结果，而不描述如何实现该结果。

 To set these properties, right-click the action and then click **Properties**. 在“属性”窗口中的相关属性中键入值。

#### <a name="local-postconditions"></a>本地后置条件
 后置条件是指在将操作视为已完成之前应先满足的条件。 在示例操作“确认订单”中，后置条件可能为：

 客户提供了处理其信用卡所需的完整有效的详细信息。

 后置条件可以表示操作发生前后的状态之间的关系。 例如:

 利息与以前相比翻倍。

 可以通过引用操作中已处理的数据的特定特性，采用更为正式的方式来编写后置条件。 例如:

 `InvoiceTotal == Sum(OrderItem.MenuItem.Price)`

#### <a name="local-preconditions"></a>本地前置条件
 前置条件是指在准备开始某个操作时应为 true 的条件。 例如，“确认订单”操作可能具有以下前置条件：

 客户已从菜单中选择至少一个菜。

### <a name="describing-calls-to-operations"></a>描述对操作的调用
 通常，操作描述的是由人员、软件或机器的任意组合来执行的工作。 但是，可以使用调用操作的操作来描述对特定软件的方法或函数的调用。

- 设置调用操作的操作的名称以指示被调用的操作，以及被调用的操作所针对的对象或组件。

- 向调用操作的操作中添加输入插针和输出插针，以描述参数和返回值。

- You can set the **Is Synchronous** property of the action to indicate whether your activity waits for the operation to complete.

  - If you set **Is Synchronous** to false, you are indicating that the flow can continue to the next action before the called operation is complete. 不应在操作中定义输出插针或传出数据流。

## <a name="Concurrent"></a> Concurrent Flows
 You can use the **Fork Node** and the **Join Node** to describe two or more threads of activities that can execute at the same time.

 ![The fork and join nodes show concurrent flows](../modeling/media/uml-actguideconcurrent.png "UML_ActGuideConcurrent")

 The effect of the **Fork Node** (1) is to divide the thread of control into two or more threads. 当上一个操作结束时，分叉输出端的所有操作便可以开始。

 A **Join Node** (2) brings concurrent threads together. The action after the **Join Node** may not start until all the actions leading to the **Join Node** are complete.

### <a name="describing-signals-and-events"></a>描述信号和事件
 可以将流程中发送信号的步骤显示为活动中的发送信号的操作。 可以将需等待特定的信号或事件后才能继续执行的步骤显示为接受事件的操作。

 例如，可能显示一个发送订单的步骤，然后再显示另一个必须在收到订单后才处理订单的步骤。

#### <a name="sending-a-signal"></a>发送信号
 使用发送信号的操作 (3) 可指示将某类信号或消息发送到其他活动或流程。 使用此操作的名称可指示操作所发送的消息的类型。

- 控制立即传递到控制流中的下一个操作（如果有）。

- 不能使用发送信号的操作来描述流程如何响应任何返回的信息。 为此，请使用单独的接受事件的操作。

- 可以显示传递到发送信号的操作的传入数据流，以指示可以将哪些数据与传出消息一起发送。 For more information, see [Describing Data Flow](#DataFlows).

#### <a name="waiting-for-a-signal-or-event"></a>等待信号或事件
 使用接受事件的操作 (4) 可指示此活动等待某些外部事件或传入消息。 使用此操作的名称可指示活动所等待的事件的类型。

- 若要显示活动在流中某个特定点等待外部事件或消息，请在活动中的适当位置绘制带有传入流的接受事件的操作。

- 若要显示活动可以随时响应外部事件或消息，请绘制不带任何传入流的接受事件的操作。 当发生指定的外部事件时，活动中将启动一个从接受事件的操作开始的新线程。

- 不能使用接受事件的操作来描述返回给信号发送方的任何值。 为此，请使用单独的发送信号的操作。

- 可以显示操作中的传出数据流，以演示活动如何处理通过信号收到的数据。 If you want to show more than one output flow, you should set the **IsUnmarshall** property of the Accept Event Action, which indicates that the action parses the incoming signal into its separate components. For more information, see [Describing Data Flow](#DataFlows).

### <a name="describing-multiple-data-flows"></a>描述多个数据流
 可以绘制随操作出现的多个控制流或对象流，以指示在操作结束时多个线程将合并。 其效果与分叉类似，只不过你可以混合使用控制流和对象流。

 下面的示例显示流入和流出操作的多个流。

 ![Parallel object flows](../modeling/media/uml-actguidemulti.png "UML_ActGuideMulti")

 当“客户提供详细信息”操作完成时，将会产生两个对象，即“送货地址”和“信用卡详细信息”。 将通过不同的操作来处理这两个对象。

 由于操作需要在其所有输入都可用后才能开始，因此最后一个操作在通向它的所有操作完成前不会开始。

### <a name="streams"></a>流
 可以使用活动图来帮助你描述管道或同时执行的一系列操作，并连续地将数据从一个操作传递到另一个操作。

 以下示例旨在阐明每个操作都可以生成对象并继续工作。 由于没有控制流，因此每个操作在收到它的第一个对象时都会启动。

 请注意，此示例中的连接线都是对象流，因为这些连接线至少有一端位于活动参数节点、对象节点或输入插针/输出插针上。

 ![A data flow](../modeling/media/uml-actguidestream.png "UML_ActGuideStream")

 1. 此示例具有三个活动参数节点，表示其输入和输出。

 2. 对象节点、输入插针和输出插针都可以表示缓冲区。 可以设置对象节点的“上限”属性以指明可同时位于缓冲区中的对象数目。

 3. 可以使用“决策”节点来显示分流，即将各个对象向下发送到不同的分支。 可以使用注释或节点标题来说明分流标准。

 4. 可以使用“分叉”节点来显示为对象制作两个或更多副本，并发送它们以供并发处理。

 5. 可以使用“联接”节点来显示将两个处理流合并成一个流。

### <a name="selection-and-transformation"></a>选择和转换
 可以指定转换并/或选择的对象流中的对象。 对象流是流入或流出插针或对象节点的流。

- 转换描述如何将进入流的对象转换为另一种类型。

- 选择描述如何仅将进入流的某些对象传输到接收操作。

  该示例演示了一个转换。 关系图 1 中的第一个操作会在一个输出插针上生成一个邮政编码。 在第二个操作中，该输出插针会连接到一个输入插针。 不过，第二个操作需要的是完全指定的地址。 另一个活动“地址查找”中指定了从一个类型到另一个类型的转换。 此转换引用自对象流的“转换”属性。 “地址查找”活动包含两个活动参数节点，一个用于传入邮政编码，另一个用于传出完整地址。

  ![Object transformation defined in another diagram](../modeling/media/uml-actguidetransform.png "UML_ActGuideTransform")

  可以通过以下两种方式指定转换或选择：

- 将注释附加到输入插针或输出插针。

  - To distinguish this description from a general comment, you can begin the comment with <\<**transformation**>> or <\<**selection**>>.

- 在单独的活动图中详细指定转换或选择。

  - 如果使用此方法，也请附加注释，以让读者明白已定义了转换。

##### <a name="to-specify-a-transformation-or-selection-in-a-separate-activity-diagram"></a>在单独的活动图中指定转换或选择

1. 创建新的活动图，在其中描述转换或选择流。

   - In **Solution Explorer**, right-click your project, point to **Add**, click **New Item**, and then click **Activity Diagram**. 针对转换或选择流，为此关系图指定一个适当的名称。 单击 **添加**。

2. 在新的关系图中：

   1. 创建两个活动参数节点，一个用于输入流，一个用于输出流。

   2. 创建与对象流相互连接的操作。 这将显示转换或选择的工作方式。

3. 在要使用转换或选择的任何关系图中：

   1. 创建一个对象流，即连接输入插针/输出插针、对象节点或活动参数节点的连接线。

   2. Right-click the object flow and then click **Properties**.

   3. In the **Transformation** or **Selection** property, select the diagram where you specified the transformation or selection flow.

   此外，可以为对象节点定义选择，也可以在各个输入插针和输出插针上定义选择。 Define a selection activity as in the previous procedure, and then set the **Selection** property of the object node, or input or output pin.

## <a name="see-also"></a>请参阅
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [Video: Capture Business Workflows by using Activity Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-4-capture-business-workflows)
