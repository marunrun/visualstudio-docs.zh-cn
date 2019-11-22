---
title: 'UML Use Case Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- diagrams - modeling, use case
- UML, use case diagrams
- diagrams - modeling, UML use case
- use case diagrams
- UML diagrams, use case
ms.assetid: b1ae8ed0-d00b-4f9b-8e23-733e09e81e9b
caps.latest.revision: 38
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7c9ccd5285f9a2744704c0ee13094a1dac31c53b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302832"
---
# <a name="uml-use-case-diagrams-guidelines"></a>UML 用例图：准则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can draw a *use case diagram* to summarize who uses your application or system, and what they can do with it. To create a UML use case diagram, on the **Architecture** menu, click **New UML or Layer Diagram**.

 For a video demonstration, see [Organizing Features into Use Cases](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-2-organizing-features-into-use-cases).

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 用例图有助于讨论和传达以下内容：

- 你的系统或应用程序与人、组织或外部系统进行交互的几种方案。

- 它帮助参与者实现的目标。

- 系统的范围。

  用例图不显示用例的详细信息：它只汇总用例、参与者和系统之间的某些关系。 特别是，用例图不显示每个用例为实现目标所执行步骤的顺序。 可以在其他关系图和文档中描述这些详细信息，这些关系图和文档可与各用例相链接。 For more information, see [Describing Use Cases in Detail](#Details) in this topic.

  为用例提供的描述将使用与系统所用于的领域相关的一些词汇，如“销售”、“菜单”和“顾客”等。 明确定义这些词汇及其关系是非常重要的，你可以借助 UML 类图来进行定义。 For more information, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md).

  用例只处理系统的功能要求。 诸如业务规则、服务质量要求和实现约束等其他要求必须另外表示。 体系结构和内部详细信息也必须另外说明。 For more information about how to define user requirements, see [Model user requirements](../modeling/model-user-requirements.md).

  本主题中使用的示例与顾客可在其上从本地餐馆订餐的网站有关。

  ![Elements in a use case diagram](../modeling/media/uml-ucovactor.png "UML_UCOvActor")

- An *actor* (1) is a class of person, organization, device, or external software component that interacts with your system. Example actors are **Customer**, **Restaurant**, **Temperature Sensor**, **Credit Card Authorizer.**

- A *use case* (2) represents the actions that are performed by one or more actors in the pursuit of a particular goal. Example use cases are **Order Meal**, **Update Menu**, **Process Payment**.

   在用例图中，用例与执行它们的参与者相关联 (3)。

- Your *system (4)* is whatever you are developing. 系统可以是小型软件组件，其中的参与者只是其他软件组件；系统也可以是完整的应用程序；系统还可以是部署在多台计算机和设备上的大型分布式应用程序套件。 Example subsystems are **Meal Ordering Website**, **Meal Delivery Business**, **Website Version 2**.

   用例图可以显示系统或其子系统支持的用例。

## <a name="BasicSteps"></a> Basic Steps for Drawing Use Case Diagrams

> [!NOTE]
> Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-create-a-new-use-case-diagram"></a>创建新的用例图

1. On the **Architecture** menu, click **New UML or Layer Diagram**.

2. Under **Templates**, click **UMLUse Case Diagram**.

3. 命名该关系图。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**, and then click **OK**.

#### <a name="to-draw-a-use-case-diagram"></a>绘制用例图

1. Drag **Subsystem** boundaries from the toolbox onto the diagram, to represent either your whole system or its major components.

    - 如果不希望描述系统或其组件支持哪些用例，用例图中可以不绘制系统边界。

    - 根据需要，拖动系统的四角将其扩大。

    - 对其适当地重命名。

2. Drag **Actors** from the toolbox onto the diagram (placing them outside any system boundary).

    - 参与者表示与你的系统进行交互的各类用户、组织和外部系统。

    - 重命名这些参与者。 For example: **Customer, Restaurant, Credit card agency.**

3. Drag **Use Cases** from the toolbox onto the appropriate systems.

    - 用例表示参与者借助你的系统所执行的活动。

    - 使用参与者自身能够理解的名称重命名这些用例。 不要使用与代码有关的名称。 For example: **Order Meal, Pay for Meal, Deliver Meal**.

    - Begin with major transactions such as **Order Meal**, leaving until later smaller interactions such as **Select Menu Item**.

    - 将每个用例放入支持它的系统或主要子系统（忽略任何只与用户有关的外观或组件）。

    - 可以在系统边界外绘制用例，以表明系统（可能在特定版本中）不支持该用例。

4. Click **Association** on the toolbox, then a use case, and then an actor that participates in the use case. 以此方式将每个参与者与其用例相链接。

5. Structure the use cases with the **Include**, **Extend** and **Generalization** relationships. 若要创建其中的每个链接，请依次单击工具、源用例和目标。 See the following section titled [Structuring Use Cases](#Structuring).

6. 详细描述用例。 See the following section titled [Describing Use Cases in Detail](#Details).

7. 绘制其他关系图，使其分别针对不同子系统或不同相关用例组。 一个建模项目中的所有关系图是同一模型的多种视图。

## <a name="Actors"></a> Drawing Actors and Use Cases
 用例图的主要用途是显示与系统交互的用户以及这些用户借助系统实现的主要目标。

- Create **Actors** to represent classes of people, organizations, other systems, software or devices that interact with your system or subsystem.

  - To learn how to draw actors and other elements, see [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

  - 对于每一组不同的目标，按其类型或角色标识参与者，即使具体的个人或实体可能是相同的。 例如，“餐馆”和“顾客”是不同的参与者，即使餐馆的雇员可能有时候也是顾客。

- Create **Use Cases** for each of the goals that each actor seeks to achieve with the system.

  - 以参与者能够理解的词语命名并描述用例，而不应使用实现术语。

- Use **Associations** to link actors to use cases.

### <a name="inheritance-between-actors"></a>参与者之间的继承
 ![Use case diagram showing inheritance](../modeling/media/uml-ucguideinherit.png "UML_UCGuideInherit")

 You can draw a **Generalization** link between Actors. 专用参与者（如示例中的“俱乐部顾客”）继承泛化参与者（如“顾客”）的用例。 箭头应指向更通用的参与者，如“顾客”。 创建链接时，首先指向更专用的参与者。

 专用参与者可以有自己的额外用例，这些用例对于其他参与者是不可用的。

> [!CAUTION]
> 不应造成会导致参与者泛化自身的泛化关系循环。 循环可能会产生错误。

### <a name="alternative-actor-icons"></a>可选参与者图标
 可以使用自定义图标而不是标准线条图来表示参与者。 例如，可以将其更改为类似于设备、餐馆和银行等的图标。

##### <a name="to-change-the-appearance-of-an-actor"></a>更改参与者的外观

1. Right-click the actor and then click **Properties**.

     此时会显示“属性”窗口。

2. Set the **Image Path** property to the location of an image file.

    - 可以使用多种图像格式的任何一种，包括 .gif、.jpg 和 .bmp。

    - 使用包含在解决方案或项目源控件中的文件，以便它在移动或复制解决方案时仍可用。

3. 若要将此外观复制到其他用例图中，请复制该参与者并将其粘贴到其他关系图中。

    - 图像的更改仅应用于特定关系图中的视图。 而不会应用于基础模型元素。 如果将参与者从 UML 模型资源管理器拖动到另一个关系图中，该参与者将以标准线条图显示。

### <a name="multiplicities-between-actors-and-use-cases"></a>参与者与用例之间的重数
 The association between an actor and a use case can show a *multiplicity* at each end.

 ![Use case one to one with actor](../modeling/media/uml-ucguidemulti1.png "UML_UCGuideMulti1")

> [!NOTE]
> The multiplicities of an association on a use case diagram are hidden if they are both **1**.

 By default, each multiplicity is **1**. 在模型的严格释义中，以顾客订餐为例，重数为 1 表示一餐只有一名顾客预订并且每名顾客一次只订一餐。

 你可以更改这些重数。

 例如:

 ![Use case showing many to many multiplicity](../modeling/media/uml-ucguidemulti2.png "UML_UCGuideMulti2")

- To state that several actors of the same class can take part in a single occurrence of a use case, set the multiplicity at the actor end of the association to **1..\*** .

   在图示中，一个或多个餐馆可参与实现同一订餐。

- To show that each actor can participate at the same time in several occurrences of a use case, set the multiplicity at the use case end of the association to **\*** .

   在图示中，每个餐馆可同时实现多个订餐。

##### <a name="to-set-multiplicities-on-an-association"></a>设置关联的重数

1. Right-click the association and then click **Properties**.

2. Expand either **First Role** or **Second Role**.

    *Role* means the element at one end of the association.

3. 设置 Multiplicity 属性，可从下表中选择：

   - **1** to state that exactly one instance of this role participates in each link.

   - **1..\*** to state that one or more instance of this role participate in each link.

   - **0..1** to state that participation is optional.

   - **\*** to state that zero or more instances of this role participate in the link.

> [!NOTE]
> 很多团队不在用例图中提供重数信息，保留重数的默认值 1， 而是在用例的其他描述中提供该信息。 在这种情况下，用例图中的所有重数都将隐藏。

### <a name="using-an-actor-or-use-case-on-multiple-diagrams"></a>在多个关系图中使用一个参与者或用例
 可以在多个关系图中显示相同的参与者和用例。 例如:

- 可以在不同关系图中描述同一参与者涉及的不同用例。

- 可以使用一个关系图来显示一个用例所关联的多个参与者和子系统，使用另一个关系图来显示如何将该用例结构化到被包括用例和扩展用例中。

##### <a name="to-show-the-same-actor-or-use-case-on-different-diagrams"></a>在不同关系图中显示相同参与者或用例

1. 在一个关系图中创建参与者或用例。

2. 创建另一个用例图。

3. Drag an actor or use case off **Model Explorer** onto the new diagram.

    > [!NOTE]
    > 如果放入新关系图的是已关联的参与者和用例，则它们之间的关联将自动显示在新关系图中。

## <a name="Details"></a> Describing use cases in detail
 用例表示：

- A goal of an actor in using the system, such as **Buy a Meal**; and

- One or more *scenarios*, that is, sequences of steps performed in pursuing the goal, such as: {**Order Meal, Pay, Deliver**}. In addition to success scenarios, there might be several exception or failure scenarios, such as **Credit Card Rejected**.

  对用例的描述可以有不同的详细程度。 在设计的早期阶段，仅在用例图上标示名称就足够了。  之后，可以编写更详细的方案描述。

  在 Visual Studio Ultimate 中，可以采用多种方法描述用例，这些方法可以分开使用，也可以一起使用：

- 将用例链接到项目中的另一个或多个关系图。

  - 活动图有助于解释包含循环、分支和并行线程的较复杂流程。 它还可以显示流程各部分之间的数据流。 For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

  - 序列图有助于解释不同参与者之间复杂的交互序列。 它还可用于显示系统内发生的对每个用例的响应。 For more information, see [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

- 将用例链接到用于详细描述用例的 OneNote 页面、节或段落。

- 将用例链接到 Word 文档，在该文档中使用文本和屏幕截图等来描述该用例的方案。 For more information, see [Model user requirements](../modeling/model-user-requirements.md).

#### <a name="to-link-a-use-case-to-a-diagram-or-file-in-the-same-solution"></a>若要将用例链接到同一解决方案中的关系图或文件

1. 绘制关系图（如序列图或活动图）来演示用例的方案。

2. 返回到用例图。

3. 将关系图或文件从解决方案资源管理器拖动到用例图的空白部分。

4. Connect from the artifact to the use case using a **Dependency**.

#### <a name="to-link-to-a-solution-file-such-as-a-word-document-or-powerpoint-presentation"></a>若要链接到诸如 Word 文档或 PowerPoint 演示文稿等解决方案文件

1. 编写一个文档，在该文档中使用文本、屏幕截图等来描述用例的方案。

2. 向解决方案中添加文档。

    1. 将该 Word 文档移入解决方案所在的 Windows 文件夹。

    2. In Solution Explorer, right-click the solution, point to **Add**, and then click **Existing Item**.

    3. Navigate to the Word document and click **Add**.

         该 Word 文档将显示在解决方案资源管理器的解决方案文件夹中。

3. 将 Word 文档从解决方案资源管理器拖动到用例图的空白部分。

     随即显示新项目。

4. Connect from the artifact to the use case using a **Dependency**.

#### <a name="to-link-to-a-shared-document-onenote-element-or-web-page"></a>若要链接到共享文档、OneNote 元素或网页

1. 获取的共享元素的 URL。 This can be, for example, a network file path beginning '\\\\', or a web page or Sharepoint URL beginning 'http://', or a link to a OneNote section, page, or paragraph beginning 'onenote:'.

2. In the Toolbox, click **Artifact** and then click in the use case diagram.

3. With the new artifact selected, type or paste the URL into the **Hyperlink** property.

> [!NOTE]
> 双击项目可打开与其链接的关系图或文档。

### <a name="linking-use-cases-to-work-items"></a>将用例链接到工作项
 If your project uses [!INCLUDE[vstsTfsRosarioLong](../includes/vststfsrosariolong-md.md)] and you have [!INCLUDE[esprtfc](../includes/esprtfc-md.md)], you can link each use case to a work item in [!INCLUDE[esprfound](../includes/esprfound-md.md)]. To learn how to make these links, see [Link model elements and work items](../modeling/link-model-elements-and-work-items.md).

 这使你能够：

- 在链接的工作项中描述用例。 特别是，如果你的项目使用 Visual Studio 正式过程模板，则可以链接到用例工作项。 此工作项类型提供对用例的目标和方案进行描述的字段。

- 将测试用例链接到用例，以便可以获取实现用例的代码开发进度的报告。

- 将任务链接到用例，以便可以跟踪开发工作的进度。

## <a name="Structuring"></a> Structuring Use Cases
 应设法只用几个主要用例来描述系统的行为。 每个大型用例定义某个参与者实现的主要目标，如购买产品，如果是从供应商的角度出发，则为提供用于销售的产品。

 明确这些目标之后，可以细化如何实现每个目标以及基本目标的变体。

 避免将用例分解得过细。 用例应基于用户对系统的体验，而不是系统内部的处理。 此外，你通常会发现，创建代码的早期工作版本比花费时间对用例进行精细的结构化更高效。

 可以在用例图中汇总主要用例和细化用例之间的关系。 以下各节对此进行介绍：

- [Showing the details of a use case with Include](#Include)

- [Sharing goals with Generalization](#Inheritance)

- [Separating out variant cases with Extend](#Extend)

### <a name="Include"></a> Showing the details of a use case with Include
 Use an **Include** relation to show that one use case describes some of the detail of another. In the illustration, **Order a Meal** includes **Pay**, **Choose Menu**, and **Choose Menu Item**. 每个被包括的细化用例是一个或多个参与者为了实现包括用例的整体目标可能必须执行的一个步骤。 箭头应指向细化的被包括用例。

> [!CAUTION]
> 不应造成会导致用例包括自身的包括关系循环。 循环可能会产生错误。

 可以共享被包括用例。 In the example, the **Order a Meal** and **Subscribe to Reviews** use cases both include **Pay**.

 ![Use cases decomposed with include](../modeling/media/uml-ucguideinclude.png "UML_UCGuideInclude")

 被包括用例的目标和方案应具有独立意义，以便可以包括在以后设计的用例中。

 将用例分为包括部分和被包括部分对于实现以下目标很有用：

- 将用例描述结构化为不同的详细层次。

- 避免在不同用例中重复共享方案。

#### <a name="Steps"></a> Defining the order of the detailed steps
 用例图不提供执行细化步骤必须遵循的顺序，也不告知其中的每一步骤是否始终是必需的。

 To make the order of the steps clear, you can use an **Artifact** to attach a separate document to the including use case. 在下面的示例中，一个活动图附加到“订餐”用例。 或者，可以使用包含步骤列表或一系列屏幕截图的文本文档。 For more information, see [Describing Use Cases in Detail](#Details).

 使用活动图时请注意下面的命名约定：

- 整个活动的名称与包括用例的名称相同。

- 活动图中的操作与被包括用例有相同的名称。

  For more information, see [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

  ![Use case steps shown in linked activity diagram](../modeling/media/uml-ucguidesteps.png "UML_UCGuideSteps")

### <a name="Inheritance"></a> Sharing goals with Generalization
 Use a Generalization relation to show that a *specialized* use case is a particular way to achieve the goals expressed by another *general* use case. 开放箭头应指向更通用的用例。

 ![Use cases showing the generalization relation](../modeling/media/uml-ucguidegeneral.png "UML_UCGuideGeneral")

 For example, **Pay** generalizes **Pay by Credit Card** and **Pay by Cash**.

> [!CAUTION]
> 不应造成会导致参与者泛化自身的泛化关系循环。 循环可能会产生错误。

 专用用例有助于展示系统实现相同目标的不同方法。

 专用用例视为继承了通用用例的目标和参与者。 通用用例可以没有自己的方案；其专用化描述实现目标的不同方法。

##### <a name="to-refactor-common-goals-from-two-or-more-use-cases"></a>通过两个或更多用例重构共同目标

1. 创建新的通用用例，并为其命名。

2. Create a **Generalization** relation with the large arrow pointing at the new general use case.

    1. Click **Generalization** in the toolbox.

    2. Click a specialized use case (**Pay by Credit Card** in the example).

    3. Click the general use case (**Pay** in the example).

3. 如果已描述专用用例的目标，则可将共同部分移入通用用例的描述。

4. 可将在专用用例之间共享的参与者移到通用用例。

### <a name="Extend"></a> Separating variant cases with Extend
 “扩展”链接用于表明一个用例可以在特定情况下向另一个用例添加功能。 箭头应指向被扩展的主用例。

 ![One use case extending another](../modeling/media/uml-ucguideextend.png "UML_UCGuideExtend")

> [!CAUTION]
> 不应造成会导致参与者泛化自身的扩展关系循环。 循环可能会产生错误。

 For example, the **Login** use case of a typical Web site can include **Register New User** - but only when the user does not already have an account.

##### <a name="to-separate-a-use-case-into-main-and-extending-parts"></a>将用例分为主要部分和扩展部分

1. 创建新的扩展用例，并为其命名。

2. Create an **Extend** relation with the arrow pointing at the extended use case.

   1. Click **Extend** in the toolbox.

   2. Click the extending use case (**Register New User** in the example).

   3. Click the extended use case (**Login** in the example).

       > [!NOTE]
       > 避免在关系图中创建扩展关系的循环。 用例不能成为自身的扩展。

3. 如果已创建被扩展用例的方案，可将相关步骤移入扩展方案。

4. The description of the extension (**Register New User** in the example) should include details of where in the main use case scenarios it will occur, and under what circumstances. 将其视为修改主用例的描述。

   扩展用例表示本应属于主用例方案一部分的方案步骤。 扩展的方案和目标将始终在主用例的上下文中读取，因此它们不需要单独有用。

   描述以下情况时，分离扩展很有用：

- 存在仅参与扩展用例的额外参与者。 例如，需要管理员来批准顾客在网站上的注册。

- 单独的子系统将处理扩展用例。

- 此扩展将只在系统的特定版本中可用。 可以在用例图中将每个版本显示为一个单独的子系统。

## <a name="Subsystems"></a> Using Subsystem Boundaries
 子系统边界用于表明哪些用例在系统的范围内。

#### <a name="to-draw-a-subsystem-boundary"></a>绘制子系统边界

1. In the toolbox, click **Subsystem**, then click the diagram.

    子系统将显示在关系图中。

2. 拖动子系统的四角以调整其大小。

3. 将现有用例拖入或拖出子系统以调整该子系统内容。

   \- 或 -

   To create a new use case directly in a subsystem, click **Use Case** in the toolbox, then click inside the subsystem.

> [!NOTE]
> The **Subjects** property of a use case indicates what subsystem it is contained within.

### <a name="use-cases-outside-the-system-scope"></a>系统范围外的用例
 将属于业务组成部分但不由你开发的系统来处理的用例包括在关系图中通常是很有用的。 这有助于开发人员了解其工作背景。 例如，“送餐”可以显示为涉及参与者“餐馆”和“顾客”的用例，但在“订餐网站”的职责范围外。

### <a name="multiple-subsystems"></a>多个子系统
 可以创建多个子系统边界，以表明不同用例是如何由不同的系统组件来处理的。 For example, **Add Restaurant Appraisal** may be dealt with on a separate forum Web site. 请记住，用例图应处理用户可见的内容。 如果要描述系统内部的工作划分，应考虑使用组件图。

### <a name="system-versions"></a>系统版本
 可以使用不同的子系统边界来演示系统的不同版本。 例如，“付款”用例可能包括在“网站版本 2”中，但不在“版本 1”中。这表示系统可帮助顾客订餐。 但是，顾客必须直接付款给餐馆。

 Use **Dependency** relations to link subsystems representing different versions or variants.

 ![Subsystems show different versions of a system](../modeling/media/uml-ucguidesystem.png "UML_UCGuideSystem")

## <a name="see-also"></a>请参阅
 [Model user requirements](../modeling/model-user-requirements.md) [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md) [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md) [Video: Organizing Features into Use Cases](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-2-organizing-features-into-use-cases)
