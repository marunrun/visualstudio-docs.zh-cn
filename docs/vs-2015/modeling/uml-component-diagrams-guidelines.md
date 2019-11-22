---
title: 'UML Component Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML diagrams, component
- diagrams - modeling, component
- diagrams - modeling, UML component
- UML, component diagrams
- component diagrams
ms.assetid: 6c1bdd60-369e-477e-83ed-7f6fe75c9f0b
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 99f2b67d264edcaab5272d0224d4450ee2e8a6f6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297163"
---
# <a name="uml-component-diagrams-guidelines"></a>UML 组件图：准则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can draw a *component diagram* to show the structure a software system. For a video demonstration, see [Designing the Physical Structure by using Component Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-6-designing-a-projects-physical-structure).

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 To create a UML component diagram, on the **Architecture** menu, click **New UML or Layer Diagram**.

 组件是可在其环境中替换的模块化单元。 Its internals are hidden, but it has one or more well-defined *provided interfaces* through which its functions can be accessed. A component can also have *required interfaces*. 所需的接口定义该组件需要其他组件中的哪些功能或服务。 将多个组件的提供的接口和所需的接口相连接，可以构造更大的组件。 完整的软件系统可以理解为是一个组件。

 绘制组件图具有以下几个好处：

- 考虑与主要块有关的设计，可帮助开发团队理解现有设计并创建新设计。

- 认为系统是具有定义完善的提供接口和所需接口的组件集合，从而可以改进组件之间的分离。 这反过来又使设计更易于理解，且在需求发生更改时可以更容易地做出相应更改。

  无论设计已在使用或将要使用的语言或平台如何，您都可以使用组件图来表示您的设计。

## <a name="OtherDiagrams"></a> Relationship to Other Diagrams
 您以将组件图与其他关系图结合使用。

|其他关系图|帮助您讨论和传达设计的这些方面|
|-------------------|--------------------------------------------------------------------|
|UML 序列图|-   Interactions between a system's components<br />-   Interactions and between the parts inside a component.<br /><br /> For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).|
|UML 类图|-   The interfaces of a component. 类图可让你详细了解接口的方法。<br />-   The data sent in parameters across the components' interfaces.<br /><br /> For more information, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).|
|活动图|-   The internal processing performed by a component in response to incoming messages.<br /><br /> For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).|
|层关系图|-   Logical architectural tiers for your components.<br /><br /> For more information, see [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md).|

## <a name="Basics"></a> Basic Steps for Drawing Component Diagrams
 For reference information about the elements on component diagrams, see [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md).

 For more information about how to use component diagrams in the process of design, see [Model your app's architecture](../modeling/model-your-app-s-architecture.md).

> [!NOTE]
> Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-create-a-component-diagram"></a>创建组件图

1. On the **Architecture** menu, click **New UML or Layer Diagram**.

2. Under **Templates**, click **UML Component Diagram**.

3. 命名该关系图。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**, and then click **OK**..

     A new component diagram appears with the UML **Component Diagram** toolbox. 该工具箱中包含所需的元素和关系。

### <a name="drawing-components"></a>绘制组件
 ![Components with interfaces](../modeling/media/uml-compdrawing.png "UML_CompDrawing")

 Create a *component* (1) for each major functional unit in your system or application.

 这方面的示例包括应用程序、硬件设备、Web 服务、.NET 程序集、程序类或一组类或者程序的任何可分段。

##### <a name="to-create-components"></a>创建组件

1. Click **Component** in the toolbox, and then click a blank part of the diagram.

     \- 或 -

     复制并粘贴现有组件。

    1. Find an existing component in a diagram or in **UML Model Explorer**.

    2. Right-click the component and then click **Copy**.

    3. 打开希望在其中显示复制的组件的关系图。

    4. Right-click a blank part of the diagram and then click **Paste**.

         组件的副本随即以新名称显示。

2. 单击组件的名称以更改它。

3. 如果您只想看到组件的标头，请单击 V 形 (5)。

### <a name="showing-the-ports-of-a-component"></a>显示组件的端口
 A *port* (2, 3) represents a group of messages or operation calls that pass either into or out of a component. 组由接口描述，而接口定义端口的类型。 端口可以提供接口也可以需要接口。

 A port with a *provided interface* (2) supplies operations that are implemented by the component, and that can be used by other components.

 这方面的示例包括用户界面、Web 服务、.NET 接口或任何编程语言中的函数集合。

 A port with a *required interface* (3) represents a component's requirement for a group of operations or services to be provided by other components or external systems.

 例如，Web 浏览器需要 Web 服务器，应用程序外接程序需要应用程序中的服务。

 组件可以具有任意数量的端口。

##### <a name="to-add-ports-to-a-component"></a>将端口添加到组件

1. In the toolbox, click **Provided Interface** or **Required Interface**.

2. 单击要将端口添加到的组件。

    端口随即显示在组件的边界上。

    新接口即作为端口的类型创建。 This interface appears in **UML Model Explorer**.

3. 沿着组件边界拖动端口以将其放置在所需位置。

4. 拖动端口的标签以调整其位置。

5. 单击该标签以更改它。 标签显示接口的名称。 如果您更改了标签，则也更改了接口的名称。

   若要列出接口的特性和操作，可在 UML 模型资源管理器中将这些特性和操作添加到接口来做到这一点。 或者，可以将接口从 UML 模型资源管理器拖动到类图上，并在此位置添加操作和特性。

### <a name="linking-between-components"></a>在组件之间进行链接
 使用依赖项 (4) 以显示一个组件的要求可以通过其他组件提供的操作或服务来满足。

##### <a name="to-show-that-a-provided-interface-can-satisfy-a-required-interface"></a>显示提供的接口可以满足所需的接口

1. In the toolbox, click **Dependency**.

2. 单击一个组件上具有所需的接口的端口，再单击另一个组件上具有提供的接口的端口。

   应尝试避免设计依赖项循环，即组中的每个组件都依赖于所有其他组件。

##### <a name="to-add-a-port-for-an-existing-interface-to-a-component"></a>将现有接口的端口添加到组件

- Find the interface in **UML Model Explorer** and then drag it from there onto the component.

     或

- 复制引用并将其粘贴到关系图中的接口。

    1. On a class diagram or a component diagram, right-click the interface and then click **Copy**.

    2. On the component diagram, right-click the component, and then click **Paste Reference**.

         提供的接口随即显示在组件上。 旁边显示了一个操作标记。

        > [!NOTE]
        > If you use **Paste** instead of **Paste Reference**, a new interface that has a new name will be created.

    3. If you wanted to create a required interface, click the Action tag and then click **Convert to Required Interface**.

## <a name="Parts"></a> Showing the Internal Parts of a Component
 ![Component diagram showing internal parts](../modeling/media/uml-compshowing.png "UML_CompShowing")

 可以将部件 (3) 放置在组件 (1) 中，以显示彼此进行交互的较小组件如何组成该组件。

 插图中的关系图指明，类型“立即就餐 Web 服务”的每个实例都包含一个“顾客服务器”实例和一个“厨房服务器”实例。

 部件是其父组件的属性，与属于普通类的特性非常类似。 部件有其自己的类型，该类型通常也是组件。 部件的标签与普通特性具有相同的形式：

 `+ partName : TypeName`

 在父组件内部，每个部件都显示了为其类型（4、5）定义的提供的接口和所需的接口。 一个部件需要的操作或服务可以由另一个部件提供。 You can use **Part Assembly** connectors to show how parts are connected with one another (6).

 还可以显示父组件的某个部件实际提供还是需要该组件的接口。 You can connect a port of the parent to a port of an internal part using a **Delegation** relation (9). 这两个端口的类型必须相同（同时为提供或所需），且其接口类型应兼容。

 可以使用新类型或通过现有类型创建新部件。

#### <a name="to-add-parts-to-a-component"></a>将部件添加到组件

1. 为您认为是父组件的部件的每个主要功能单元创建一个部件。

    1. Click **Component** in the toolbox, and then click inside the parent component (1).

         新部件 (3) 随即显示在父组件中。

         A new component is created in **UML Model Explorer**. 此组件是新部件的类型。

         \- 或 -

         将现有组件从 UML 模型资源管理器拖动到父组件。

         新部件 (3) 随即显示在父组件中。 其类型为从 UML 模型资源管理器拖动的组件。

         \- 或 -

         Right-click a component, either in a diagram or in UML Model Explorer, and then click **Copy**.

         Right-click on the parent component, and then click **Paste Reference**.

         新部件 (3) 随即显示在父组件中。 其类型为所复制的组件。

    2. 单击新部件的名称以更改它。 您无法更改该部件的类型。

    3. 可以将提供的接口和所需的接口（4、5）添加到新部件。 Click the **Provided Interface** or **Required Interface** tool, and then click in the part.

         \- 或 -

         Drag an existing interface from **UML Model Explorer** onto the part.

         接口随即添加到部件的类型，并显示在部件本身上。 父组件会根据需要调整接口的大小。

2. 将部件相互连接。

    - Use the **Dependency** tool to connect the ports of different parts (6).

3. 将部件连接到父组件的端口：

    1. 在父组件上创建一个或多个端口 (7)。 Click **Required Interface** or **Provided Interface** on the toolbox, and then click the parent component.

    2. 将端口委托 (9) 给一个或多个部件。 Click the **Delegation** tool, then a port on the parent component, and then a port on a part. 可以通过相同方式连接提供接口或需要接口的端口。

### <a name="showing-the-parts-of-a-part"></a>显示部件的多个部件
 将组件分解为多个部件后，可以将每个部件类型分解为其自己的内部部件。

 在单独的组件图中分解每个层最为简单。 首先必须找到部件的类型。 如插图所示，一个部件名为 `DNCustomerServer`，且其类型是称为 `CustomerServer` 的组件。 可以在 UML 模型资源管理器中找到该类型，并将其放置在其他关系图中。 然后，您可以创建该类型自己的内部部件。

##### <a name="to-place-a-parts-type-on-a-diagram"></a>将部件的类型放置到关系图上

1. 确定部件的类型的完全限定名。

     Right-click the part and then click **Properties**.

     The type name appears in the **Type** field of the Properties window.

2. Locate the part's type in **UML Model Explorer**.

     Click **View**, point to **Other Windows**, and then click **UML Model Explorer**.

     展开项目和该类型所属的任何包（如果需要）。

     The type will be listed as a **Component**.

     如果需要，可以在此处更改类型的名称。

3. 打开或创建另一个组件图。

4. 从 UML 模型资源管理器中的类型拖动到该关系图上。

     类型的视图显示为关系图中的组件。

     该组件具有的接口与您为部件定义的接口相同。

     现在可以向组件中添加部件。

## <a name="Designing"></a> Designing the Component

### <a name="describing-how-the-parts-collaborate"></a>介绍部件的协作方式
 您可以绘制一个序列图，以显示各部件如何协同工作以响应到达父组件的消息。

 可以使用这些关系图来解释现有组件并设计新组件。

 如果您仍要设计组件，则可以先绘制一些序列图，然后再确定该组件将包含哪些部件。 可以使用这些序列图体验不同的部件、所需的接口和消息序列。 为最常用且最重要的传入消息绘制序列图。 然后可以在组件中创建与您已确定的生命线对应的部件。

 使用序列图可以判断系统的工作在不同组件之间是如何分布的。

- 如果一个部件上堆集了太多工作，则与在各个部件之间平均分布工作相比，应用程序可能更难更新。

- 如果工作在多个交互操作之间分布得非常稀疏，则系统在执行时可能会出错且可能会难以理解。

  ![Sequence diagram showing collaborating parts](../modeling/media/uml-compdescparts.png "UML_CompDescParts")

##### <a name="to-draw-a-sequence-diagram-that-shows-collaboration-between-parts"></a>绘制显示各部件间的协作的序列图

1. 创建新的序列图。

     For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

2. 为向组件发送消息的外部组件、用户、设备或其他参与者 (1) 创建生命线。

     You can set the **Actor** property of this lifeline to true, to indicate that it is external to the component under consideration. 在生命线上方会出现一个简图。

3. 为所选参与者向其发送消息的组件的提供的接口 (2) 创建生命线。

4. 为组件的每个部件 (3) 创建生命线。

5. 为组件的每个所需的接口 (4) 创建生命线。

6. 基于外部参与者 (5) 绘制消息。 显示如何将消息传递给部件以及部件如何协同工作以响应消息。

7. 根据需要，显示发送到所需的接口 (6) 的消息。 不必显示执行消息时的任何详细信息。

### <a name="is-the-component-more-than-its-parts"></a>组件是否比其部件要多？
 在某些情况下，组件只是为部件集合指定的名称。 所有工作都由部件完成，在运行时，没有任何表示组件的代码或其他项目。

 You can indicate this in the model by setting the **Is Indirectly Instantiated** property of the component. 在这种情况下，组件的所有接口都应位于端口上，且委托给内部部件。

### <a name="describing-the-process-inside-each-part"></a>介绍每个部件内的进程
 可以使用活动图显示组件处理每个传入消息的方式。 For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

 ![Activity diagram with data buffer](../modeling/media/uml-compdescribingproc.png "UML_CompDescribingProc")

 使用“接受事件操作”(1) 显示传入消息启动新线程。

 使用对象节点和输入/输出指针显示信息流和信息的存储位置。 在示例中，对象节点 (2) 用于显示正在各个线程之间缓冲的项。

### <a name="defining-data-and-classes"></a>定义数据和类
 可以使用 UML 类图描述以下方面的详细内容：

- 组件的接口。 在将 requires 或 provides 端口添加到组件时，接口将显示在 UML 模型资源管理器中。 你可以将此接口拖动或复制到 UML 类图中，以显示其特性和操作以及与其他接口的关系。

- 在接口的操作参数中传递的数据。

- 组件中存储的数据，例如活动图的对象流中所示。

### <a name="general-dependencies-between-components"></a>组件之间的普通依赖项
 使用组件图只是显示设计的主要部件及其相互依赖项。

 ![A dependency between components](../modeling/media/uml-compdepend.png "UML_CompDepend")

 Use the **Dependency** tool to draw a dependency. 这指示一个组件的设计依赖于另一个组件。

 依赖项具有以下典型类型：

- 一个组件调用另一个组件中的代码。

- 一个组件实例化在另一个类中定义的类。

- 一个组件使用另一个组件创建的信息。

  您可以使用依赖项箭头的名称来表示特定类型的使用情况。 To set the name, right-click the arrow, then click **Properties**, and set the **Name** field in the properties window.

## <a name="see-also"></a>请参阅
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [Video: Designing the Physical Structure by using Component Diagrams](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-6-designing-a-projects-physical-structure)
