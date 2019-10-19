---
title: UML 序列图：准则 |Microsoft Docs
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
ms.openlocfilehash: 88c72ecaf44855badfd42456d9818f2ba9168a49
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661728"
---
# <a name="uml-sequence-diagrams-guidelines"></a>UML Sequence Diagrams: Guidelines
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可以绘制*序列图*来显示交互。 交互是类、组件、子系统或参与者的典型实例之间的消息序列。

 UML 序列图是 UML 模型的一部分，并且仅存在于 UML 建模项目中。 若要创建 UML 序列图，请在 "**体系结构**" 菜单上单击 "**新建 UML 或层关系图**"。 大致了解有关[uml 序列图元素](../modeling/uml-sequence-diagrams-reference.md)或[uml 建模图](../modeling/edit-uml-models-and-diagrams.md)的详细信息。 有关视频演示，请参阅[使用序列图进行草绘交互（2010）](http://channel9.msdn.com/Blogs/clinted/UML-with-VS-2010-Part-7-Sketching-Interactions-with-Sequence-Diagrams)。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="in-this-topic"></a>在本主题中
 [使用 UML 序列图](#Using)

 [绘制序列图的基本步骤](#BasicSteps)

 [创建和使用简单序列图](#Simple)

 [类和生命线](#ClassesAndLifelines)

 [创建可重用交互序列](#Multiple)

 [折叠生命线组](#Collapse)

 [用片段描述控制结构](#Fragments)

## <a name="Using"></a>使用 UML 序列图
 序列图可在不同的程序详细信息级别用于实现各种用途。 需要绘制序列图的典型情况如下所示：

- 如果拥有汇总了系统用户及其目标的用例图，则可以绘制序列图，用于描述系统的主要组件如何交互以实现每个用例的目标。 有关详细信息，请参阅[UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)。

- 如果已标识到达组件接口的消息，则可以绘制序列图，用于描述组件的内部部件如何交互以实现每个传入消息所需的结果。 有关详细信息，请参阅[UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)。

  绘制序列图有以下几个好处：

- 可以轻松了解任务在组件之间的分布方式。

- 可以识别使软件更新变得困难的交互模式。

## <a name="relationship-to-other-diagrams"></a>与其他关系图的关系
 可以通过多种方法组合使用 UML 序列图和其他关系图。

#### <a name="lifelines-and-types"></a>生命线和类型
 在序列图中绘制的生命线可以表示系统中的组件或类的典型实例。 可以根据类型创建生命线，也可以根据生命线创建类型，并且可以在 UML 类图和 UML 组件图中显示类型。 有关详细信息，请参阅[类和生命线](#ClassesAndLifelines)。

#### <a name="parameter-types"></a>参数类型
 对于在生命线之间发送的消息中使用的参数类型和返回值，也可以在 UML 类图中进行描述。

#### <a name="use-case-details"></a>用例详细信息
 用例表示用户的目标以及实现该目标的步骤序列。 可以通过多种方法描述步骤序列。 一种方法是绘制显示用户与系统主要组件之间的交互的序列图。 有关详细信息，请参阅[UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)。

## <a name="BasicSteps"></a>绘制序列图的基本步骤
 有关序列图上的元素的完整列表，请参阅[UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)。

> [!NOTE]
> [编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)中介绍了如何创建任何建模图的详细步骤。

#### <a name="to-create-a-sequence-diagram"></a>创建序列图

1. 在 "**体系结构**" 菜单上，单击 "**新建 UML 或层关系图**"。

2. 在 "**模板**" 下，单击 " **UML 序列图**"。

3. 命名该关系图。

4. 在 "**添加到建模项目**" 中，选择解决方案中的现有建模项目，或者**创建一个新的建模项目**，然后单击 **"确定"** 。

    此时会出现一个新的序列图，其中包含**序列图**工具箱。 该工具箱中包含所需的元素和连接线。

   ![序列图的各个部分](../modeling/media/uml-sequence.png "UML_Sequence")

#### <a name="to-draw-a-sequence-diagram"></a>绘制序列图

1. 将**生命线**（1）从**工具箱**拖到关系图上，以表示类、组件、参与者或设备的实例。

    > [!NOTE]
    > 还可以通过将现有类、接口、参与者或组件从**UML 模型资源管理器**拖到关系图上来创建生命线。 这将创建一个表示所选类型的实例的生命线。

2. 绘制消息，用于显示生命线如何协作以实现特定目标。

     要创建消息（3、4、6、7），请单击消息工具。 然后在希望消息开始的位置单击发送生命线，然后单击接收生命线。

     此时接收生命线上将显示执行发生 (5)。 执行发生表示实例执行方法的一段时间。 可以创建从执行发生开始的其他消息。

3. 要显示来自未知事件源 (9) 或传播给未知接收方 (10) 的消息，请绘制一个起始于或终止于关系图上的空白区域的异步消息。 这些消息称为 "*找到消息*（9）" 和 "*丢失消息*（10）"。

    > [!NOTE]
    > 若要移动具有丢失的消息或找到的消息的一组生命线，请先按照以下步骤选择生命线，然后再移动它们：在这些生命线周围绘制一个矩形，或按住**CTRL**键的同时单击每个生命线。 如果使用 "**全选**"或 CTRL **+ 选择**所有生命线，然后移动它们，则附加到这些生命线的任何丢失的消息或找到的消息将不会移动。 如果出现这种情况，你可以单独移动这些消息。

4. 为相同组件或系统的每个主要消息绘制序列图。

#### <a name="to-change-the-order-of-messages"></a>更改消息的顺序

- 在消息的生命线中向上或向下拖动该消息。 可以将它拖动到其他消息上方，也可以将它拖入或拖出执行块。

     \- 或 -

- 单击该消息，然后使用**向上**键和**向下**键调整消息位置。 使用**shift + 向上键**和**shift + 向下键**可更改消息的顺序。

#### <a name="to-move-or-copy-message-sequences-on-the-sequence-diagram"></a>在序列图上移动或复制消息序列

1. 右键单击消息（3，4），然后单击 "**复制**"。

2. 右键单击要从其发送新消息的执行发生（5）或生命线（1），然后单击 "**粘贴**"。 新发送方可以位于其他关系图上（如果需要）。

     消息及其所有附属消息的副本将添加到执行发生或生命线的结尾。

    > [!NOTE]
    > 粘贴的消息始终在执行发生或生命线的结尾显示。 粘贴消息之后，可以将它向上拖动到更早的位置。

#### <a name="to-display-and-edit-the-signature-text-for-a-message"></a>显示和编辑消息的签名文本

- 必须将目标生命线绑定或映射到类型，以便让签名文本可见。 要完成此任务，请执行以下步骤之一：

  - 右键单击生命线，然后选择 "**创建类**"。

     或

  - 选择生命线，按**F4**，然后在 "**属性**" 窗口中，将 "**类型**" 属性设置为现有类型或指定新类型的名称。 右键单击 "消息" 标签，然后选择 "**创建操作**"。

    此时消息标签下将显示签名文本。 现在可以编辑签名文本。 有关详细信息，请参阅[类和生命线](#ClassesAndLifelines)。

#### <a name="to-improve-the-layout-of-a-sequence-diagram"></a>改进序列图的布局

- 右键单击关系图的空白部分，然后单击 "**重新排列布局**"。

- 若要撤消操作，请单击 "**编辑**"，然后单击 "**撤消**"。

#### <a name="to-change-the-package-that-owns-the-interaction"></a>更改拥有交互的包

1. 在 " **UML 模型资源管理器**" 中，查找序列图显示的交互。

    > [!NOTE]
    > 在将第一个生命线添加到序列图上之前，不会在 " **UML 模型资源管理器**" 中显示交互。

2. 将交互拖动到包中。

     \- 或 -

     右键单击交互，然后单击 "**剪切**"。 右键单击该包，然后单击 "**粘贴**"。

## <a name="Simple"></a>创建和使用简单序列图
 最简单且使用最广泛的序列图格式只包含生命线和消息。 使用此类关系图，你可以清晰地显示设计中各对象之间或系统及其用户之间的典型交互序列。 这通常足够帮助你讨论和沟通设计。

 下面是在绘制简单序列图时需要考虑的一些事项。

### <a name="types-of-message"></a>消息的类型
 可以使用三种工具创建消息。

- 使用**同步**工具描述发送方等待接收方返回响应的交互（3）。

     在执行发生结束时，将显示一个 **< \<return > >** 箭头。 它指示控制回到发送方。

- 使用**异步**工具描述发送方可以立即继续的交互，而不会等待接收方（4）。

- 使用 "**创建**" 工具描述发送方创建接收方（8）的交互。

     创建消息应是接收方接收的第一个消息。

### <a name="annotating-the-interactions"></a>对交互进行批注
 若要描述有关序列的详细信息，可以在关系图上的任何位置放置**注释**。

 使用**注释链接**，可以将注释链接到生命线、执行、交互使用和片段。

> [!CAUTION]
> 如果想要将注释附加到序列中的特定位置，则需将它链接到执行发生、交互使用或片段。 请不要将注释链接到生命线，因为在这种情况下，注释不会保持附加在序列中的正确位置。

 使用注释可以：

- 注明已在序列中的关键位置实现的目标。 这有助于读者查看交互的目标。

- 描述整个序列的整体目标。 将注释附加到初始执行发生或不进行附加。 例如，“客户已从菜单中点菜并获得报价”。

- 描述每个生命线的职责。 将注释附加到生命线。 例如，“订单管理器收集客户的菜单选择”。

- 注明可能作为所示典型序列的替代项执行的异常或替代项。 例如，“客户可以选择跳过此序列的其余部分”。

  - 请考虑使用片段作为此类注释更为正式的替代项。 请参阅[用片段描述控制结构](#Fragments)

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

- 使用[描述控件结构和片段](#Fragments)来显示循环、替代项等。

## <a name="assessing-the-design"></a>评估设计
 可以使用该关系图评估任务在其对象或组件之间的分布情况。 如果看到下列模式，请考虑进行重构：

- 一个生命线似乎在执行所有操作，调用其他所有内容，而另一个生命线只是被动响应。

- 许多消息跨越生命线。 每个生命线应仅向邻近的几个生命线发送消息，不应与其邻近生命线的邻近生命线通信。 通常应该可以排列生命线，以便消息只在几个位置跨越生命线；在具有交点的位置，目标生命线还不应交换跨越了生命线的消息。

- 某些生命线似乎在处理多种类型的任务。 应该可以轻松找到描述每个生命线的职责的简洁句子，其中汇总了生命线响应其接收的每个消息时所做的工作。

## <a name="ClassesAndLifelines"></a>类和生命线
 序列图中的生命线显示类或组件接口的实例。 可以通过两种方法命名生命线：

|**出于此目的**|**使用此格式**|
|--------------------------|-------------------------|
|类型的匿名实例。<br /><br /> 如果每个类型只有一个生命线，则使用这种格式。|*typeName*|
|类型的命名实例。<br /><br /> 如果想要显示涉及同一类型的多个实例的序列，则使用此格式。|*objectName*：*typeName*|

### <a name="creating-lifelines-from-types"></a>根据类型创建生命线
 例如，你可以根据已在类图中定义的类创建新生命线。

> [!NOTE]
> 执行此任务之前，请确保已拥有现有序列图。

##### <a name="to-create-a-lifeline-from-an-existing-type"></a>根据现有类型创建生命线

- 将类、组件或接口从 UML 模型资源管理器拖动到序列图中。

   \- 或 -

  1. 右键单击相应关系图上的类、组件或接口，然后单击 "**创建生命线**"。

  2. 在 "**创建生命线**" 对话框中，选择一个序列图，然后单击 **"确定"** 。

     此时将显示新的命名实例生命线，其类型为你拖动的类型。

  > [!NOTE]
  > 可以根据需要多次重复此操作。 这将创建具有不同实例名的生命线。

##### <a name="to-change-the-type-of-a-lifeline"></a>更改生命线的类型

1. 右键单击生命线，然后单击 "**属性**"。

2. 在 "**属性**" 窗口中，设置 "**类型**" 属性。 可以从下拉菜单中选择一个类型，也可以键入新名称。

### <a name="creating-classes-from-lifelines"></a>根据生命线创建类
 如果已创建一个或多个序列图，则可以通过根据这些序列图创建类或接口来汇总生命线。

##### <a name="to-create-a-class-or-interface-from-a-lifeline"></a>根据生命线创建类或接口

1. 右键单击生命线，然后单击 "**创建类**" 或 "**创建接口**"。

     此时 UML 模型资源管理器中将显示新类或新接口。

2. 在生命线接收到的每个消息的类或接口中创建操作：

    1. 选择想要包括的所有消息。

    2. 右键单击其中一条消息，然后单击 "**创建方法**"。

         新类或新接口具有每个选定消息的操作。

         操作名称将显示在每个消息箭头和消息的 "**操作**" 属性中。

         如果消息包括“（参数 : 类型）”形式的参数，则它们将在新操作的参数列表中显示。

        > [!NOTE]
        > 如果要在序列图中添加新消息，则必须重复此步骤。

3. 要查看新类或新接口的详细信息，请将其添加到类图或组件图中。

    1. 打开或创建一个类图或组件图。

    2. 将新类或接口从 " **UML 模型资源管理器**" 拖动到类图。

         此时类图中将显示新类或新接口。

         \- 或 -

    3. 将新接口从 " **UML 模型资源管理器**" 拖动到组件图中的组件或端口上。

         接口将在组件上显示为棒糖形。

### <a name="creating-classes-for-parameters"></a>创建参数的类
 可以在序列图上的消息中包括参数。 可以使用 UML 类图描述参数类型。

## <a name="Multiple"></a>创建可重用交互序列
 可以使用单独的关系图描述包含想要分离出去的或几个关系图共有的详细信息的序列。

 可以在一个关系图上创建指向另一个关系图中的详细信息的交互使用矩形 (12)。

 双击一个交互使用，打开链接到它的序列图。

#### <a name="to-create-a-reusable-interaction-sequence-from-existing-lifelines"></a>根据现有生命线创建可重用交互序列

1. 在**工具箱**中，单击 "**交互使用**"。

2. 在序列图上，按住鼠标按钮，拖过想要包括在可重用序列中的生命线。 从想要在其中插入交互使用的垂直位置开始。

     交互使用将在序列图上的选定生命线中显示。

3. 双击交互使用上的名称，将其重命名为描述此关系图中可重用序列效果的名称。

     \- 或 -

     使用参数编写类似函数调用的名称。

4. 将交互使用链接到另一个序列图。 右键单击交互使用，然后：

     单击 "新建**序列**" 以创建新的序列图

     \- 或 -

     单击 "**链接到序列**" 以链接到现有关系图。

     Visual Studio 将在交互使用和新交互序列之间创建一个链接。

     此时解决方案中将显示新序列图。 它包含你用于创建交互使用的生命线。

    > [!NOTE]
    > 新关系图将只包括你用于创建交互使用的生命线。 新关系图将不包括在交互使用之后创建的生命线，即使交互使用现在覆盖这些生命线。

#### <a name="to-create-a-reusable-sequence-from-existing-messages"></a>根据现有消息创建可重用序列

- 右键单击要移动的消息，然后单击 "**移动到关系图**"。

  Visual Studio：

  - 用交互使用替换选定消息及任何附属消息。

  - 将替换的消息移动到新序列图。

  - 在交互使用和新序列图之间创建一个链接。

#### <a name="to-navigate-to-the-sequence-referenced-by-an-interaction-use"></a>导航到交互使用引用的序列

- 双击交互使用。

     \- 或 -

     右键单击交互使用，然后单击 "**前往序列**"。

### <a name="creating-a-placeholder-with-an-interaction-use"></a>使用交互使用创建占位符
 可以创建交互使用而不将其链接到另一个关系图。 您可以使用此占位符作为序列的一部分，其详细信息尚未处理。使用交互使用的名称来指示所需的结果。

## <a name="Collapse"></a>折叠生命线组
 可以将一组生命线折叠到一起，以便该组显示为一个生命线。 这有助于你将一组对象可视化为单个组件。 折叠组中的生命线之间的消息和交互使用处于隐藏状态。 包括其他生命线的消息和交互序列处于显示状态。

#### <a name="to-collapse-a-group-of-lifelines-together"></a>将一组生命线折叠到一起

1. 选择两个或多个生命线。

2. 右键单击其中一个，然后单击 "**折叠**"。

     这些单独的生命线将替换为一个生命线。

     仅涉及组成员的消息和交互使用处于隐藏状态。

3. 要重命名组，请单击名称。

    > [!NOTE]
    > 展开组时，组名将丢失。

#### <a name="to-expand-a-collapsed-group"></a>展开折叠的组

- 右键单击折叠的生命线，然后单击 "**展开**"。

    > [!NOTE]
    > 组的名称以及从该组到注释或工作项的任何链接都将丢失。

## <a name="Fragments"></a>用片段描述控制结构
 可以使用组合片段 (13) 定义序列图中的循环、分支和并发处理。 或者，可以考虑改用活动图。 活动图在显示参与者之间的消息时不太有用，但某些情况下，在显示循环、分支和并发时比较有用。

 有关片段类型的完整列表，请参阅[使用 UML 序列图上的片段描述控制流](../modeling/describe-control-flow-with-fragments-on-uml-sequence-diagrams.md)。

#### <a name="to-create-a-combined-fragment"></a>若要创建组合片段

1. 选择一个消息，或消息序列（其中所有消息都在同一执行发生或生命线上开始）。

    > [!NOTE]
    > 选择消息箭头，而不要选择消息指向的执行发生。

2. 右键单击其中一条消息，指向 "**外侧代码**"，然后单击所需的片段类型。

     此时将显示新片段。 它包含你选择的消息。

     如果组合片段类型允许多个片段，则也将显示空片段。

3. 若要设置片段的临界，请右键单击片段边框，然后单击 "**属性**"。 设置 "**临界**" 属性。

     临界用于定义分支或循环的条件。

4. 若要将新片段添加到允许多个片段的类型，请右键单击片段的边界，然后指向 "**添加**"。 单击 "前后的**交互操作数** **"。**

5. 要将新消息添加到片段中，请使用消息工具，或者使用复制和粘贴。

## <a name="see-also"></a>请参阅
 [Uml 序列图：引用](../modeling/uml-sequence-diagrams-reference.md)[编辑 uml 模型和关系图](../modeling/edit-uml-models-and-diagrams.md) [UML 用例图：引用](../modeling/uml-use-case-diagrams-reference.md) [Uml 类图](../modeling/uml-class-diagrams-reference.md)：引用 uml[组件图](../modeling/uml-component-diagrams-reference.md)：引用 uml[组件图](../modeling/uml-component-diagrams-reference.md) [：引用视频：使用序列图的草绘交互](http://go.microsoft.com/fwlink/?LinkId=201113)
