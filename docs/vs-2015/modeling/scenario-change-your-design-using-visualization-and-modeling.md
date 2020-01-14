---
title: 方案：使用可视化和建模更改设计 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- code visualization [Visual Studio ALM]
- modeling software [Visual Studio ALM]
- software modeling [Visual Studio ALM]
- walkthroughs [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], modeling software
- walkthroughs [Visual Studio ALM], modeling software
ms.assetid: ccc80825-a4a0-44fa-a0bb-f95254785a3b
caps.latest.revision: 63
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 70cc3c81c426ec55d0afb36360155786ec97d937
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918983"
---
# <a name="scenario-change-your-design-using-visualization-and-modeling"></a>方案：使用可视化和建模更改设计
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用 Visual Studio 中的可视化和建模工具，确保你的软件系统满足用户的需求。 使用统一建模语言 (UML) 关系图、代码图、层关系图和类图等工具执行以下操作：

 若要查看支持每个工具的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

- 阐明用户需求和业务流程。

- 可视化和浏览现有代码。

- 描述对现有系统所做的更改。

- 验证系统是否满足其要求。

- 使代码与设计保持一致。

  本演练：

- 介绍这些工具可为软件项目带来的好处。

- 演示如何在示例方案中使用这些工具（无论你的开发方法如何）。

  要了解有关这些工具及其支持的方案的详细信息，请参阅：

- [体系结构分析和建模](../modeling/analyze-and-model-your-architecture.md)

- [代码可视化](../modeling/visualize-code.md)

- [为应用程序创建模型](../modeling/create-models-for-your-app.md)

## <a name="ScenarioOverview"></a> 方案概述
 本方案介绍了 Dinner Now 和 Lucerne Publishing 这两家虚构公司的软件开发周期中的各个阶段。 Dinner Now 在西雅图提供基于 Web 的送餐服务。 客户可以在 Dinner Now 网站上订餐和付费。 订单随后会发送给相应的本地餐馆以便其配送餐点。 Lucerne Publishing 是一家位于纽约的公司，在网上和网下经营了多项业务。 例如，他们运营了一家网站，客户可以在这个网站上发表自己对餐馆的评论。

 Lucerne 最近收购了 Dinner Now，并希望进行以下变革：

- 通过将餐馆评论功能添加到 Dinner Now 来整合其网站。

- 将 Dinner Now 的支付系统更换为 Lucerne 的系统。

- 将 Dinner Now 服务推广到整个区域。

  Dinner Now 使用 SCRUM 和 eXtreme Programming。 他们的测试覆盖率非常高，不受支持的代码非常少。 他们通过创建小巧而有效的系统版本，然后逐步添加功能，从而最大程度地减小风险。 他们通过短期而频繁的迭代来开发代码。 这样一来，他们便自信地接受更改、经常重构代码并避免“初期进行大量设计”。

  Lucerne 保留了一组很复杂的大型系统，其中有一些系统已有 40 年以上的历史。 由于旧版代码很复杂且涉及范围很广，因此他们对更改非常谨慎。 他们遵循一个更严格的开发过程，希望设计详细的解决方案并记录开发过程中进行的设计和更改。

  这两个团队都使用 Visual Studio 中的建模图来帮助自己开发满足用户需求的系统。 他们借助 Team Foundation Server 和其他工具来计划、整理和管理其工作。

  有关 Team Foundation Server 的详细信息，请参阅：

- [计划和跟踪工作](#PlanningTracking)

- [测试、验证和签入更新的代码](#TestValidateCheckInCode)

## <a name="ModelingDiagramsTools"></a> 体系结构关系图和建模图在软件开发中的角色
 下表描述了这些工具在软件开发生命周期的各个阶段中可扮演的角色：

||**用户需求建模**|**业务流程建模**|**系统体系结构和设计**|**代码可视化和浏览**|**确认**|
|------|------------------------------------|-----------------------------------|--------------------------------------|------------------------------------------|----------------------|
|用例图 (UML)|√|√|||√|
|活动图 (UML)|√|√|√||√|
|类图 (UML)|√|√|√||√|
|组件图 (UML)|√|√|√||√|
|序列图 (UML)|√|√|√||√|
|域特定语言 (DSL) 图|√|√|√|||
|层关系图，层验证|||√|√|√|
|代码图|||√|√|√|
|类设计器（基于代码）||||√||

 要绘制 UML 关系图和层关系图，你必须将建模项目创建为现有解决方案的一部分或创建一个新的建模项目。 这些关系图必须在建模项目内创建。 UML 关系图上的项是某个常见模型的一部分，而 UML 关系图是该模型的视图。 层关系图上的项位于建模项目中，但未存储在常见模型中。 根据代码创建的代码图和 .NET 类图存在于建模项目外部。

 请参阅：

- [创建 UML 建模项目和关系图](../modeling/create-uml-modeling-projects-and-diagrams.md)

- [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

- [如何：向项目中添加类图（类设计器）](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)

- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

  要显示体系结构的替代视图，你可以在多个或不同的关系图上重用同一模型中的某些元素。 例如，你可以将一个组件拖动到另一个组件图或一个序列图上，这样该组件便可作为一个参与者。 请参阅[编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)。

  这两个团队还使用层验证来确保正在开发的代码与设计保持一致。

  请参阅：

- [使代码与设计保持一致](#ValidatingCode)

- [描述逻辑体系结构：层关系图](#DescribeLayers)

- [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

  > [!NOTE]
  > 某些版本的 Visual Studio 支持层验证以及代码图和 UML 关系图的只读版本以进行可视化和建模。 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="UnderstandingCommunicating"></a> 了解和传达系统相关信息
 由于没有规定 Visual Studio 建模图的使用顺序，因此你可以根据自己的需求和方法来使用它们。 通常，团队会在整个项目中反复而频繁地重新访问其模型。 每个关系图都有自己的长处，可帮助你理解、描述和沟通正在开发的系统的各方面问题。

 Dinner Now 和 Lucerne 通过将关系图作为其公共语言来互相沟通以及与项目利益干系人沟通。 例如，Dinner Now 使用关系图执行以下任务：

- 可视化现有代码。

- 就新的用户情景或更新的用户情景与 Lucerne 进行沟通。

- 确定支持新的用户情景或更新的用户情景必需的更改。

  Lucerne 使用关系图执行以下任务：

- 了解 Dinner Now 的业务流程。

- 了解系统的设计。

- 就新的用户需求或更新的用户需求与 Dinner Now 进行沟通。

- 记录对系统进行的更新。

  关系图与 Team Foundation Server 集成在一起，方便团队更轻松地计划、管理和跟踪其工作。 例如，他们使用模型来确定测试用例和开发任务以及估算其工作量。 Lucerne 将 Team Foundation Server 工作项链接到模型元素，以便能监视进度并确保系统满足用户需求。 例如，他们将用例链接到测试用例工作项，这样在所有测试都通过时，他们便能知道用例满足要求。

  团队在签入其更改之前，会运行包含层验证和自动测试的生成来对测试和设计验证代码。 这有助于确保更新的代码不会与设计发生冲突且不会中断之前运行的功能。

  请参阅：

- [了解系统在业务流程中的角色](#UnderstandingBPMandSystemDesign)

- [描述新的或更新的用户需求](#DescribingURM)

- [从模型创建测试](#CreatingTests)

- [标识对现有系统所做的更改](#DeterminingChanges)

- [Keeping code consistent with the design](#ValidatingCode)

- [创建和使用模型的一般提示](#GeneralTips)

- [计划和跟踪工作](#PlanningTracking)

- [测试、验证和签入更新的代码](#TestValidateCheckInCode)

### <a name="UnderstandingBPMandSystemDesign"></a>了解系统在业务流程中的角色
 Lucerne 希望了解有关 Dinner Now 业务流程的详细信息。 他们创建了以下关系图，以便更轻松地阐明他们所掌握的有关 Dinner Now 的信息：

|**关系图**|**描述**|
|-----------------|-------------------|
|*用例图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)<br />-   [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)|-晚餐系统支持的活动<br />-执行活动的人员和外部系统<br />-系统中支持每个活动的主要组件<br />-位于当前系统范围之外的业务流程部分，例如食物交付|
|*活动图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)<br />-   [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)|客户创建订单时发生的步骤流|
|*类图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)<br />-   [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)|讨论中使用的业务实体和术语以及这些实体之间的关系。 例如，在本方案中，订单和菜单项是词汇表的一部分。|

 例如，Lucerne 创建了以下用例图，以便理解 Dinner Now 网站上执行的任务及其执行者：

 ![UML 用例图](../modeling/media/uml-usecase.png "UML_UseCase")

 **UML 用例图**

 下面的活动图介绍了客户在 Dinner Now 网站上创建订单时的步骤流。 在此版本中，注释元素用于识别角色，行用于创建 *“泳道”* ，而泳道可按角色整理步骤：

 ![UML 活动图](../modeling/media/uml-dinnernowprocess.png "UML_DinnerNowProcess")

 **UML 活动图**

 下面的类图介绍了参与订购过程的实体：

 ![UML 类图](../modeling/media/uml-dinnerorders.png "UML_DinnerOrders")

 **UML 类图**

### <a name="DescribingURM"></a>描述新的或更新的用户需求
 Lucerne 希望向 Dinner Now 系统添加相关功能，以便客户能阅读和发表餐馆评论。 他们更新了以下关系图，以便能描述此新需求并与 Dinner Now 进行讨论：

|**关系图**|**描述**|
|-----------------|-------------------|
|*用例图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)<br />-   [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)|针对“写餐馆评论”的新用例|
|*活动图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)<br />-   [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)|客户希望写餐馆评论时发生的步骤|
|*类图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)<br />-   [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)|存储评论必需的数据|

 例如，下面的用例图包含新的“写评论”用例以表示新需求。 为了更加便于识别，它在关系图上突出显示为橙色：

 ![UML 用例图](../modeling/media/uml-writerev.png "UML_WriteRev")

 **UML 用例图**

 下面的活动图包含显示为橙色的新元素，以描述新用例中的步骤流：

 ![UML 活动图](../modeling/media/uml-writereview.png "UML_WriteReview")

 **UML 活动图**

 下面的类图包含一个新的 Review 类以及它与其他类的关系，以便团队能讨论其详细信息。 请注意，一位客户和一家餐馆可以有多条评论：

 ![UML 类图](../modeling/media/uml-dinnerreviews.png "UML_DinnerReviews")

 **UML 类图**

### <a name="CreatingTests"></a>从模型创建测试
 两个团队都同意，他们在进行任何更改前都需要对系统及其组件进行一套完整的测试。 Lucerne 安排了一个专业团队来执行系统和组件级测试。 他们会重用由 Dinner Now 创建的测试并使用 UML 关系图构建这些测试：

- 每个用例都由一个或多个测试表示。 用例图上的元素会链接到 Team Foundation Server 中的测试用例工作项。

- 活动图或系统级序列图上的每个流至少要链接到一个测试。 测试团队能系统地确保他们对活动图中每条可能的路径进行测试。

- 用于描述测试的术语基于由用例、类和活动图定义的术语。

  由于需求发生了更改，并且已更新关系图来反映这些更改，因此也会更新测试。 只有通过了测试，才会认为已满足需求。 在可能或可行的情况下，将在实现开始之前根据 UML 关系图定义测试。

  请参阅：

- [基于模型开发测试](../modeling/develop-tests-from-a-model.md)

- [验证 UML 模型](../modeling/validate-your-uml-model.md)

### <a name="DeterminingChanges"></a> Identifying Changes to the Existing System
 Dinner Now 必须估计满足新的需求所需的成本。 这部分取决于此更改将对系统的其他部件造成的影响的程度。 为了帮助他们了解这一点，Dinner Now 的一位开发人员根据现有代码创建了以下代码图和关系图：

|**代码图或关系图**|**显示**|
|------------------------|---------------|
|*代码图*<br /><br /> 请参阅：<br /><br /> -   [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br />-   [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)<br />-   [通过编辑 DGML 文件自定义代码图](../modeling/customize-code-maps-by-editing-the-dgml-files.md)|代码中的依赖关系以及其他关系。<br /><br /> 例如，Dinner Now 首先会查看程序集代码图，大致了解这些程序集及其依赖关系。 他们可以深入探讨代码图，浏览这些程序集中的命名空间和类。<br /><br /> Dinner Now 还可以创建代码图来浏览特定区域和代码中其他类型的关系。 他们借助解决方案资源管理器来帮助查找和选择感兴趣的区域和关系。|
|*基于代码的类图*<br /><br /> 请参阅 [How to: Add Class Diagrams to Projects (Class Designer)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)。|代码中的现有类|

 例如，开发人员创建一个代码图。 她调整了该代码图的范围，以侧重于将受到新方案影响的区域。 代码图上选中并突出显示了这些区域：

 ![命名空间依赖项关系图](../modeling/media/namespace-reviewsystem.png "Namespace_ReviewSystem")

 **命名空间代码图**

 开发人员展开选定命名空间以查看其类、方法和关系：

 ![展开的命名空间依赖项关系图](../modeling/media/dep-reviewsystem.png "Dep_ReviewSystem")

 **带可见跨组链接的已展开的命名空间代码图**

 开发人员检查代码以查找受影响的类和方法。 要在进行更改的同时查看所做每项更改的影响，请在做出每项更改后重新生成代码图。 请参阅[可视化代码](../modeling/visualize-code.md)。

 要描述对系统其他部分（如组件或交互）进行的更改，团队可以在白板上绘制这些元素。 这两个团队还可以在 Visual Studio 中绘制以下关系图，以捕获、管理和了解详细信息：

|**关系图**|**描述**|
|------------------|-------------------|
|*活动图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)<br />-   [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)|系统通知客户重新从餐馆下订单时发生的步骤流，用于提示客户写评论。|
|*类图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)<br />-   [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)|逻辑类及其关系。 例如，添加一个新类来描述 **“评论”** 以及它与其他实体（如 **“餐馆”** 、 **“菜单”** 和 **“客户”** ）的关系。<br /><br /> 要将评论与客户关联，系统必须存储客户详细信息。 UML 类图可帮助阐明这些详细信息。|
|*基于代码的类图*<br /><br /> 请参阅 [How to: Add Class Diagrams to Projects (Class Designer)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)。|代码中的现有类。|
|*组件图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)<br />-   [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)|系统的高级部分，如 Dinner Now 网站及其接口。 这些接口定义组件如何通过他们提供和使用的方法或服务来互相交互。|
|*序列图（UML）*<br /><br /> 请参阅：<br /><br /> -   [UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)<br />-   [UML 序列图：准则](../modeling/uml-sequence-diagrams-guidelines.md)|实例间的交互的序列。|

 例如，下面的组件图演示了新组件，该组件是 Dinner Now 网站组件的一部分。 ReviewProcessing 组件可处理用于创建评论的功能，该组件突出显示为橙色：

 ![UML 组件图](../modeling/media/uml-internal.png "UML_Internal")

 **UML 组件图**

 下面的序列图演示了交互的序列，这些交互是在 Dinner Now 网站检查客户之前是否已从餐馆下单时出现的。 如果客户之前已从餐馆下单，该网站会要求客户创建评论，该评论随后会发送给餐馆并发布到网站上：

 ![UML 序列图](../modeling/media/uml-revsystem.png "UML_RevSystem")

 **UML 序列图**

### <a name="ValidatingCode"></a> 使代码与设计保持一致
 Dinner Now 必须确保更新的代码与设计保持一致。 他们创建了描述系统中的功能层的层关系图，指定了这些层之间可存在的依赖关系，并将解决方案项目关联到了这些层。

|**关系图**|**描述**|
|-----------------|-------------------|
|*层关系图*<br /><br /> 请参阅：<br /><br /> -   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：参考](../modeling/layer-diagrams-reference.md)<br />-   [层关系图：准则](../modeling/layer-diagrams-guidelines.md)<br />-   [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|代码的逻辑体系结构。<br /><br /> 层关系图会将 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中的项目整理并映射到名为 *“层”* 的抽象组中。 这些层可标识这些项目在系统中执行的角色、任务或功能。<br /><br /> 层关系图可用于描述系统的预期设计并对该设计验证相关代码。<br /><br /> 要创建层，请从解决方案资源管理器、代码图、类视图和对象浏览器中拖动项。 要绘制新层，请使用工具箱或右键单击关系图图面。<br /><br /> 要查看现有依赖关系，请右键单击层关系图图面，然后单击“生成依赖项”。 要指定预期的依赖关系，请绘制新的依赖关系。|

 例如，下面的层关系图描述了各个层之间的依赖关系以及每个层关联的项目数：

 ![集成支付系统的层关系图](../modeling/media/layer-integrated-dnlucerne.png "Layer_Integrated_DNLucerne")

 **层关系图**

 为确保代码开发过程中不与设计发生冲突，团队对 Team Foundation Build 上运行的生成使用了层验证。 他们还创建了自定义 MSBuild 任务以要求在其签入操作中进行层验证。 他们使用生成报告来收集验证错误。

 请参阅：

- [定义生成过程](https://msdn.microsoft.com/library/61593e10-d24b-492f-b19a-af4d85abea6b)

- [使用封闭签入生成过程以验证更改](https://msdn.microsoft.com/library/9cfc8b9c-1023-40fd-8ab5-1b1bd9c172ec)

- [自定义生成过程模板](https://msdn.microsoft.com/library/b94c58f2-ae6f-4245-bedb-82cd114f6039)

### <a name="GeneralTips"></a> General Tips for Creating and Using Models

- 大多数关系图都是由用线连接的节点组成的。 对于每种关系图类型，工具箱提供了不同类型的节点和线。

   要打开工具箱，请在“视图” 菜单上单击“工具箱”。

- 要创建节点，请将它从工具箱拖动到关系图上。 必须将某些类型的节点拖动到现有节点上。 例如，在组件图上，必须将新端口添加到现有组件。

- 要创建线或连接，请在工具箱中单击相应的工具，再单击源节点，然后单击目标节点。 有些线只能在某些类型的节点之间创建。 当你将指针移动到可能的源或目标上方时，指针会指示你是否能创建连接。

- 当你在 UML 关系图上创建项时，也会将这些项添加到常见模型中。 建模项目中的 UML 关系图是该模型的视图。 层关系图上的项是建模项目的一部分，即使它们未存储在常见模型中。

   要查看模型，在“体系结构” 菜单上，指向“Windows”，然后单击“UML 模型资源管理器”。

- 在某些情况下，可以将某些项从“UML 模型资源管理器” 拖动到 UML 关系图上。 可在多个或不同的关系图上使用同一模型中的某些元素，来显示体系架构的替代视图。 例如，你可以将一个组件拖动到另一个组件图或一个序列图上，以作为参与者使用。

- Visual Studio 支持 UML 2.1.2。 本概述仅介绍此版本中的 UML 关系图的主要功能，但有很多书籍详细讨论了 UML 及其用法。

  请参阅[创建应用模型](../modeling/create-models-for-your-app.md)。

### <a name="PlanningTracking"></a> Planning and Tracking Work
 Visual Studio 建模图与 Team Foundation Server 集成在一起，方便你更轻松地计划、管理和跟踪工作。 两个团队使用模型来确定测试用例和开发任务以及估算其工作量。 Lucerne 创建了 Team Foundation Server 工作项并将其链接到模型元素（如用例或组件）。 这有助于他们监视进度和跟踪为满足用户需求所做的工作。 这有助于他们确保所做的更改仍能满足这些需求。

 在开展工作时，团队会更新其工作项以反映他们在各自的任务上所花费的时间。 他们还会使用以下 Team Foundation Server 功能来监视和报告工作状态：

- 每日 *“燃尽报表”* ，显示他们是否将在预期时间完成计划的工作。 他们会从 Team Foundation Server 生成其他类似的报表以跟踪 Bug 的进度。

- *“迭代工作表”* ，使用 Microsoft Excel 来帮助团队监视和权衡其成员的工作负荷。 此工作表链接到 Team Foundation Server，并提出团队日常进度会议上讨论的重点。

- *“开发仪表板”* ，使用 Office Project 来告知团队重要的项目信息。

  请参阅：

- [使用 Visual Studio Team Services 或 Team Foundation Server 跟踪工作](https://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)

- [链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)

- [适用于 Visual Studio ALM 的图表、仪表板和报表](https://msdn.microsoft.com/library/1f28ba6c-c5e5-46d3-9209-ede24ae78e48)

- [使用 Project 创建积压工作 (backlog) 和任务](https://msdn.microsoft.com/library/be5cef4f-755f-4ffe-8dd7-876d1e02c330)

### <a name="TestValidateCheckInCode"></a> 测试、验证和签入代码
 当团队完成每个任务时，他们会将其代码签入 Team Foundation 版本控制，如果他们忘记这样做，则会收到来自 Team Foundation Server 的提醒。 在 Team Foundation Server 接受团队的签入前，团队会运行单元测试和层验证以根据测试用例和设计来验证代码。 他们使用 Team Foundation Server 来定期运行生成、自动单元测试和层验证。 这有助于确保代码满足以下条件：

- 有效。

- 不会中断之前运行的代码。

- 不会与设计发生冲突。

  Dinner Now 提供了大批自动测试，Lucerne 可以重用这些测试，因为它们几乎都仍适用。 Lucerne 也可以基于这些测试进行生成并添加新测试以涵盖新的功能。 两个均使用 Visual Studio 运行手动测试。

  要确保代码与设计保持一致，团队需在 Team Foundation Build 中配置生成以加入层验证。 如果发生任何冲突，系统会生成包含详细信息的报告。

  请参阅：

- [测试应用程序](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)

- [在开发过程中验证系统](../modeling/validate-your-system-during-development.md)

- [使用版本控制](/azure/devops/repos/tfvc/overview?view=azure-devops)

- [生成应用程序](/azure/devops/pipelines/index)

## <a name="UpdatingSystem"></a> Updating the System Using Visualization and Modeling
 Lucerne 和 Dinner Now 必须集成其支付系统。 以下各部分介绍了可帮助团队执行此任务的 Visual Studio 建模图:

- [了解用户需求：用例图](#UnderstandUseCases)

- [了解业务流程：活动图](#UnderstandActivities)

- [描述系统结构：组件图](#DescribeComponents)

- [描述交互：序列图](#DescribeSequence)

- [可视化现有代码：代码图](#VisualizeCode)

- [定义类型的术语表：类图](#DefineClasses)

- [描述逻辑体系结构：层关系图](#DescribeLayers)

  请参阅：

- [为应用程序创建模型](../modeling/create-models-for-your-app.md)

- [代码可视化](../modeling/visualize-code.md)

- [在你的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)

- [建立用户需求模型](../modeling/model-user-requirements.md)

- [应用体系结构建模](../modeling/model-your-app-s-architecture.md)

### <a name="UnderstandUseCases"></a>了解用户需求：用例图
 用例图汇总了系统支持的活动以及这些活动的执行者。 Lucerne 通过用例图来了解有关 Dinner Now 系统的以下信息：

- 客户创建订单。

- 餐馆接收订单。

- Dinner Now 支付系统用来验证支付的外部支付处理器网关超出了网站的范围。

  该关系图还演示了如何将某些主要用例划分为较小的用例。 Lucerne 希望使用自己的支付系统。 他们用不同的颜色突出显示“处理付款”用例以指示该用例需要更改：

  ![突出显示用例图上的 "处理付款"](../modeling/media/uml-processpay.png "UML_ProcessPay")

  **在用例图上突出显示 "处理付款"**

  如果开发时间较短，则团队可能会讨论是否要让客户直接付款给餐馆。 为了说明这一点，他们会将“处理付款”用例替换为一个 Dinner Now 系统边界外的用例。 然后，他们会将客户直接链接到餐馆，指示 Dinner Now 只处理订单：

  ![用例图上的支付餐费付款餐馆](../modeling/media/uml-payrestaurant.png "UML_PayRestaurant")

  **用例图上的支付餐费付款餐馆**

  请参阅：

- [UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)

- [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)

#### <a name="drawing-a-use-case-diagram"></a>绘制用例图
 用例图具有以下主要功能：

- *“参与者”* 表示由人员、组织、计算机或软件系统扮演的角色。 例如，“客户”、“餐馆”和“Dinner Now 支付系统”都是参与者。

- *“用例”* 表示参与者和正在开发的系统之间的交互。  从一次鼠标单击或一条消息到延续多天的事务，它们能表示任何规模的交互。

- *“关联”* 将参与者与用例链接在一起。

- 一个大型用例可 *“包含”* 多个小型用例，例如“创建订单”包含“选择餐馆”。 你可以 *“扩展”* 用例（这将向扩展后的用例添加目标和步骤）以指示用例仅在某些条件下出现。 用例也可以相互继承。

- *“子系统”* 表示正在开发的软件系统或该系统的某个组件。 它是一个包含用例的大型框。 用例图阐明了子系统边界内部或外部的内容。 要指明用户必须以其他方式完成特定目标，可在子系统边界外部绘制这些用例。

- *“项目”* 将关系图上的元素链接到其他关系图或文档。

  请参阅：

- [UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)

- [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)

#### <a name="summary-strengths-of-use-case-diagrams"></a>摘要：用例图的优点
 用例图可帮助你可视化：

- 系统支持或不支持的活动

- 执行这些活动的人员和外部系统

- 系统中支持每个活动的主要组件，可以将其表示为嵌套在父系统中的子系统

- 如何将用例划分为较小的用例或变体

#### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系

|**关系图**|**描述**|
|-----------------|-------------------|
|活动图|用例中的步骤流和该用例中这些步骤的执行者。<br /><br /> 用例的名称常常反映为活动图中的步骤。 活动图支持决策、合并、输入和输出、并发流等元素。<br /><br /> 请参阅：<br /><br /> -   [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)<br />-   [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)|
|序列图|用例中参与者之间的交互的序列。<br /><br /> 请参阅：<br /><br /> -   [UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)<br />-   [UML 序列图：准则](../modeling/uml-sequence-diagrams-guidelines.md)|
|类图 (UML)|参与用例的实体或类型。<br /><br /> 请参阅：<br /><br /> -   [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)<br />-   [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)|

### <a name="UnderstandActivities"></a>了解业务流程：活动图
 活动图描述业务流程中的步骤流并提供沟通工作流的简单方法。 开发项目可以包含多个活动图。 通常，活动包含从一个外部操作产生的所有操作，如订餐、更新菜单或将新餐馆添加到业务。 活动也可以描述复杂操作的详细信息。

 Lucerne 更新以下活动图来演示 Lucerne 如何处理付款并向餐馆付款。 他们将 Dinner Now 支付系统替换为 Lucerne 支付系统，如突出显示部分所示：

 ![活动图上的 Lucerne 支付系统](../modeling/media/uml-lucerne.png "UML_Lucerne")

 **替换活动图上的 "立即就餐" 付款系统**

 更新的关系图可帮助 Lucerne 和 Dinner Now 直观显示 Lucerne 支付系统适用于业务流程中的哪个步骤。 在此版本中，注释用于标识执行步骤的角色。 行用于创建 *“泳道”* ，而泳道可以按角色整理步骤。

 团队也可以考虑讨论一种替代情景，即客户在发送订单后改为直接向餐馆付款。 这将对软件系统提出不同的要求。

 以前，Dinner Now 在白板上或 PowerPoint 中绘制这些关系图。 他们现在还使用 Visual Studio 来绘制这些关系图，以便两个团队都能捕获、了解和管理详细信息。

 请参阅：

- [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)

- [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)

#### <a name="drawing-an-activity-diagram"></a>绘制活动图
 活动图具有以下主要功能：

- *“初始节点”* ，可指示活动的第一个操作。

   关系图应始终具有这些节点中的某个节点。

- *“操作”* ，可描述用户或软件在哪些步骤中执行任务。

- *“控制流”* ，可显示操作之间的流。

- *“决策节点”* ，可表示流中的条件分支。

- *“分叉节点”* ，可将单个流划分为并发流。

- *“活动最终节点”* ，可指示活动的结束。

   尽管这些节点是可选的，但将它们包含在关系图上来显示活动的结束位置会很有用。

  请参阅：

- [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)

- [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)

#### <a name="summary-strengths-of-activity-diagrams"></a>摘要：活动图的优点
 活动图可帮助你可视化和描述业务、系统或程序的操作之间的控制流和信息。 当与他人进行沟通时，通过此方式描述工作流既简单又实用。

#### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系

|**关系图**|**描述**|
|-----------------|---------------------|
|用例图|汇总每个参与者执行的活动。<br /><br /> 请参阅：<br /><br /> -   [UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)<br />-   [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)|
|组件图|将系统可视化为一个可重用部件的集合，这些部件通过一组定义完善的接口来提供或使用行为。<br /><br /> 请参阅：<br /><br /> -   [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)<br />-   [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)|

### <a name="DescribeComponents"></a>描述系统结构：组件图
 组件图将系统描述为一个可分离部件的集合，这些部件通过一组定义完善的接口来提供或使用行为。 部件的规模不限，并且可以通过任何方式进行连接。

 为了帮助 Lucerne 和 Dinner Now 可视化和讨论系统的组件及其接口，他们创建了以下组件图：

 ![支付系统中的外部组件](../modeling/media/uml-extdnpayment.png "UML_ExtDNPayment")

 **现在晚餐支付系统的组件**

 此关系图显示了不同的组件类型及其 *“依赖关系”* 。 例如，Dinner Now 网站和 Lucerne 支付系统都需要外部支付处理器网关来验证付款。 各个组件之间的箭头表示依赖关系，这些依赖关系指示哪些组件需要其他组件的功能。

 要使用 Lucerne 支付系统，则必须将 Dinner Now 网站更新为使用 Lucerne 支付系统上的 PaymentApproval 和 PayableInsertion 接口。

 下面的关系图显示了 Dinner Now 网站的组件的特定配置。 此配置指示网站的任何实例都包含以下四个 *“部件”* ：

- “CustomerProcessing”

- “OrderProcessing”

- “ReviewProcessing”

- “PaymentProcessing”

  这些部件是指定组件类型的实例，并将按以下方式连接：

  ![现在晚餐网站中的组件](../modeling/media/uml-dinnernow.png "UML_DinnerNow")

  **现在晚餐网站中的组件**

  Dinner Now 网站将其行为委派给这些部件，而这些部件将控制网站的功能。 父组件与其成员组件之间的箭头显示 *“委派”* ，而委派指示哪些部件处理父组件通过其接口接收或发送的消息。

  在此配置中，PaymentProcessing 组件将处理客户付款。 因此，必须更新此组件以便与 Lucerne 的支付系统集成。 在其他方案中，同一个父组件中可能有某个组件类型的多个实例。

  请参阅：

- [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)

- [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)

#### <a name="drawing-a-component-diagram"></a>绘制组件图
 组件图具有以下主要功能：

- *“组件”* ，可表示系统功能的可分离项。

- *“提供的接口端口”* ，可表示组件实现的并由其他组件或外部系统使用的消息或调用组。

- *“必需的接口端口”* ，可表示组件发送给其他组件或外部系统的消息或调用组。 此类端口描述了一个组件至少期望从其他组件或外部系统获得的操作。

- *“部件”* 是组件的成员，并且通常是其他组件的实例。 部件是父组件的内部设计的一部分。

- *“依赖关系”* ，可指示组件需要其他组件的功能。

- *“委派”* ，可指示组件中用于处理由父组件发送或接收的消息的部件。

  请参阅：

- [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)

- [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)

#### <a name="summary-strengths-of-component-diagrams"></a>摘要：组件图的优点
 组件图可帮助你：

- 将系统可视化为一个可分离部件的集合，无论其实现语言或样式如何。

- 可视化带有定义完善的接口的组件，使设计更易于理解，并在需要更改时更易于更新。

#### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系

|**关系图**|**描述**|
|-----------------|---------------------|
|代码图|可视化现有代码中的组织和关系。<br /><br /> 要标识候选组件，请创建代码图并按项在系统中的功能对其进行分组。<br /><br /> 请参阅：<br /><br /> -   [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)|
|序列图|可视化组件或组件内的部件之间的交互的序列。<br /><br /> 要在序列图上从一个组件创建生命线，请右键单击该组件，然后单击“创建生命线”。<br /><br /> 请参阅：<br /><br /> -   [UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)<br />-   [UML 序列图：准则](../modeling/uml-sequence-diagrams-guidelines.md)|
|类图 (UML)|定义提供的或必需的端口上的接口以及实现组件功能的类。<br /><br /> 请参阅：<br /><br /> -   [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)<br />-   [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)|
|层关系图|描述与组件相关的系统的逻辑体系结构。 使用层验证来确保代码与设计保持一致。<br /><br /> 请参阅：<br /><br /> -   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：参考](../modeling/layer-diagrams-reference.md)<br />-   [层关系图：准则](../modeling/layer-diagrams-guidelines.md)<br />-   [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|
|活动图|可视化组件执行的用于响应传入消息的内部处理。<br /><br /> 请参阅：<br /><br /> -   [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)<br />-   [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)|

### <a name="VisualizeCode"></a> 可视化现有代码：代码图
 代码图显示代码中的当前组织和关系。 项由代码图上的 *“节点”* 表示，而关系由 *“链接”* 表示。 代码图可帮助你执行以下各类任务：

- 探究不熟悉的代码。

- 了解建议的更改发生的位置以及这些更改可能对现有代码产生的影响的程度。

- 查找复杂区域、自然层或模式或者其他可能从改进中受益的区域。

  例如，Dinner Now 必须估计更新 PaymentProcessing 组件所需的成本。 这部分取决于此更改将对系统的其他部件造成的影响的程度。 为了帮助他们了解这一点，Dinner Now 的一位开发人员根据代码生成了代码图，并调整了范围以侧重于可能受更改影响的区域。

  下面的代码图显示了 PaymentProcessing 类和 Dinner Now 系统的其他部件之间的依赖关系，这些关系显示为选定状态：

  ![晚餐支付系统的依赖项关系图](../modeling/media/dep-dnpayment.png "Dep_DNPayment")

  **Dinner Now 支付系统的代码图**

  开发人员通过扩展 PaymentProcessing 类并选择其成员来浏览代码图，以查看可能受影响的区域：

  ![PaymentProcessing 和依赖项内的方法](../modeling/media/depgraph-expandeddn.png "DepGraph_ExpandedDN")

  **PaymentProcessing 类中的方法及其依赖关系**

  他们为 Lucerne 支付系统生成以下代码图，以检查其类、方法和依赖关系。 团队发现，Lucerne 系统可能也需要与 Dinner Now 的其他部件进行交互：

  ![Lucerne 支付系统的依赖项关系图](../modeling/media/depgraph-lucernepay.png "DepGraph_LucernePay")

  **Lucerne 支付系统的代码图**

  两个团队一起确定了集成两个系统所必需的更改。 他们决定重构某些代码以使其更易于更新。 PaymentApprover 类将移动到 DinnerNow.Business 命名空间并需要某些新方法。 处理事务的 Dinner Now 类将有自己的命名空间。 团队创建并使用工作项来计划、整理和跟踪其工作。 必要时，他们会将工作项链接到模型元素。

  在重组代码后，团队生成了一个新的代码图以查看更新的结构和关系：

  ![带有重组代码的依赖项关系图](../modeling/media/depgraph-integrated.png "DepGraph_Integrated")

  **带有重组代码的代码图**

  此代码图显示 PaymentApprover 类现在位于 DinnerNow.Business 命名空间中，并且此类具有一些新的方法。 Dinner Now 事务类现在有了自己的 PaymentSystem 命名空间，这样它稍后便能更轻松地处理代码了。

#### <a name="creating-a-code-map"></a>创建代码图

- 通过按照以下步骤进行操作来生成一个代码图，可以快速了解源代码：

     在“体系结构” 菜单上，单击“针对解决方案生成代码图”。

     要快速了解编译的代码，请创建一个空白代码图，然后将程序集文件或二进制文件拖动到该代码图图面上。

- 要了解特定代码或解决方案项，请使用解决方案资源管理器来选择要可视化的项和关系。 然后，你可以生成新的代码图或向现有代码图添加选定项。 请参阅 [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md)。

- 为了帮助你浏览代码图，请重新排列布局，使其适合你要执行的各类任务。

     例如，要要可视化代码中的分层，请选择树布局。 请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

#### <a name="summary-strengths-of-code-maps"></a>摘要：代码图的优点
 代码图可帮助你：

- 了解现有代码中的组织和关系。

- 标识可能受建议的更改影响的区域。

- 查找复杂区域、模式、层或其他可以通过改进来使代码更易于维护、更改和重用的区域。

#### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系

|**关系图**|**描述**|
|-----------------|-------------------|
|层关系图|系统的逻辑体系结构。 使用层验证来确保代码与设计保持一致。<br /><br /> 为了有助于标识现有层或预期层，请创建代码图并对相关项进行分组。 要创建层关系图，请参阅：<br /><br /> -   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：准则](../modeling/layer-diagrams-guidelines.md)|
|组件图|组件、组件的接口以及它们之间的关系。<br /><br /> 为了有助于标识组件，请创建代码图并按项在系统中的功能对其进行分组。<br /><br /> 请参阅：<br /><br /> -   [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)<br />-   [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)|
|类图 (UML)|类、类的属性和操作以及它们之间的关系。<br /><br /> 为了有助于标识这些元素，请创建一个显示这些元素的 UML 类图。<br /><br /> 请参阅：<br /><br /> -   [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)<br />-   [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)|
|类图（基于代码）|针对某个特定项目的代码中的现有类。<br /><br /> 要可视化和修改代码中的现有类，请使用类设计器。<br /><br /> 请参阅 [How to: Add Class Diagrams to Projects (Class Designer)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)。|

### <a name="DescribeSequence"></a>描述交互：序列图
 序列图描述系统的各个部件之间的一系列交互。 部件的规模不限。 例如，从一个程序中的单个对象到大型子系统或外部参与者，都可以作为部件。 交互的规模和类型不限。 例如，其范围可以从单一消息到扩展的事务，也可以是函数调用或 Web 服务消息。

 为了帮助 Lucerne 和 Dinner Now 描述和讨论“处理付款”用例中的步骤，他们根据组件图创建了以下序列图。 生命线镜像 Dinner Now 网站组件及其部件。 出现在生命线之间的消息将紧跟组件图上的连接：

 !["处理付款" 用例的序列图](../modeling/media/umlsequence-processpayment.png "UMLSequence_ProcessPayment")

 **"处理付款" 用例的序列图**

 序列图将显示客户创建订单的时间，Dinner Now 网站对 OrderProcessing 的实例调用 ProcessOrder。 接下来，OrderProcessing 对 PaymentProcessing 调用 ProcessPayment。 此过程将继续，直到外部支付处理器网关验证该支付。 仅在此情况下，控件才会返回到 Dinner Now 网站。

 Lucerne 必须估计将其支付系统更新为与 Dinner Now 系统集成所需的成本。 为了有助于了解这一点，他们还可以创建代码图来可视化受影响的代码。

 请参阅：

- [UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)

- [UML 序列图：准则](../modeling/uml-sequence-diagrams-guidelines.md)

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

#### <a name="drawing-a-sequence-diagram"></a>绘制序列图
 序列图具有以下主要功能：

- 垂直 *“生命线”* ，可表示软件对象的参与者或实例。

   要添加参与者符号（它指示参与者位于正在开发的系统的外部），请单击生命线。 在“属性” 窗口中，将“参与者” 设置为“True”。 如果未打开“属性” 窗口，请按 **F4**。

- 水平 *“消息”* ，可表示方法调用、Web 服务消息或其他一些通信。 *“执行发生”* ，它是显示在生命线上带阴影的垂直矩形，并可表示接收对象处理调用的时间段。

- 在*同步*消息期间，发送方对象会等待控制 <，\<返回 > > 与常规函数调用中一样。 在 *“异步”* 消息过程中，发送方可以立即继续。

- 使用 <\<创建 > > 消息，以指示按其他对象构造对象。 它应是发送给相关对象的第一条消息。

  请参阅：

- [UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)

- [UML 序列图：准则](../modeling/uml-sequence-diagrams-guidelines.md)

#### <a name="summary-strengths-of-sequence-diagrams"></a>摘要：序列图的优点
 序列图可帮助你可视化：

- 执行用例的过程中在参与者或对象之间传输的控制流。

- 方法调用或消息的实现。

#### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系

|**关系图**|**描述**|
|-----------------|---------------------|
|类图 (UML)|定义生命线表示的类以及在生命线之间发送的消息中使用的参数和返回值。<br /><br /> 要根据生命线创建类，请右键单击生命线，然后单击“创建类” 或“创建接口”。 要根据类图上的某个类型创建生命线，请右键单击该类型，然后单击“创建生命线”。<br /><br /> 请参阅：<br /><br /> -   [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)<br />-   [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)|
|组件图|描述生命线表示的组件以及提供和使用由消息表示的行为的接口。<br /><br /> 要根据组件图创建生命线，请右键单击该组件，然后单击“创建生命线”。<br /><br /> 请参阅：<br /><br /> -   [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)<br />-   [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)|
|用例图|在序列图上汇总用户和组件之间的交互作为一个用例，该用例表示用户的目标。<br /><br /> 请参阅：<br /><br /> -   [UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)<br />-   [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)|

### <a name="DefineClasses"></a> 定义类型的术语表：类图
 类图定义参与系统的实体、术语或概念以及它们之间的关系。 例如，可以在开发过程中使用这些关系图来描述每个类的属性和操作，无论其实现语言或样式如何。

 为了帮助 Lucerne 描述和讨论参与“处理付款”用例的实体，他们绘制了以下类图：

 ![类图中的 "处理付款" 实体](../modeling/media/uml-payentities.png "UML_PayEntities")

 **类图中的“处理付款”实体**

 此关系图显示一个“客户”可以有多个订单和不同的订单支付方式。 BankAccount 和 CreditCard 都继承自“付款”。

 在开发过程中，Lucerne 使用以下类图来描述和讨论每个类的详细信息：

 ![类图中的 "处理付款" 实体详细信息](../modeling/media/uml-payment.png "UML_Payment")

 **类图中的“处理付款”详细信息**

 请参阅：

- [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)

- [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)

#### <a name="drawing-a-class-diagram"></a>绘制类图
 类图具有以下主要功能：

- 类、接口和枚举等类型：

  - *“类”* ，它是拥有相同的特定结构特征或行为特征的对象的定义。

  - *“接口”* ，可定义对象的外部可见行为的一部分。

  - *“枚举”* ，它是包含一个文本值列表的分类器。

- *“属性”* ，它是描述 *“分类器”* 的每个实例的某个类型的值。 分类器是类型、组件、用例甚至参与者的一般名称。

- *“操作”* ，它是分类器的实例可执行的方法或函数。

- *“关联”* ，指示两个分类器之间的某种关系。

  - *“聚合”* ，它是指示两个分类器之间的共享所有权的关联。

  - *“复合”* ，它是指示分类器之间的整体-部分关系的关联。

    要显示聚合或复合，请设置关联上的“聚合” 属性。 “共享” 可显示聚合，“复合” 可显示复合。

- *“依赖关系”* ，指示更改一个分类器的定义可能会更改另一个分类器的定义。

- *“泛化”* ，指示特定分类器从通用分类器继承部分定义。 *“实现”* ，指示类将实现由接口提供的操作和属性。

   要创建这些关系，请使用“继承” 工具。 也可以将实现表示为 *“棒糖形”* 。

- *“包”* ，它是一组分类器、关联、生命线、组件和其他包。 *“导入”* 关系，指示一个包中包括另一个包的所有定义。

  作为探究和讨论现有类的第一步，你可以使用类设计器来根据代码创建类图。

  请参阅：

- [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)

- [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)

- [如何：向项目中添加类图（类设计器）](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)

#### <a name="summary-strengths-of-class-diagrams"></a>摘要：类图的优点
 类图可帮助你定义：

- 一个常用术语词汇表，在讨论用户需求和参与系统的实体时将使用它。 请参阅[模型用户需求](../modeling/model-user-requirements.md)。

- 由系统部件使用的类型（如组件），无论其实现如何。 请参阅为[应用程序的体系结构建模](../modeling/model-your-app-s-architecture.md)。

- 类型之间的关系，如依赖关系。 例如，你可以指明可将一个类型与另一个类型的多个实例关联。

#### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系

|**关系图**|**描述**|
|-----------------|---------------------|
|用例图|定义用于描述用例中的目标和步骤的类型。<br /><br /> 请参阅：<br /><br /> -   [UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)<br />-   [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)|
|活动图|定义通过对象节点、输入插针、输出插针和活动参数节点传递的数据的类型。<br /><br /> 请参阅：<br /><br /> -   [UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)<br />-   [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)|
|组件图|描述组件、组件的接口以及它们之间的关系。 类也可以描述一个完整的组件。<br /><br /> 请参阅：<br /><br /> -   [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)<br />-   [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)|
|层关系图|定义与类相关的系统的逻辑体系结构。<br /><br /> 使用层验证来确保代码与设计保持一致。<br /><br /> 请参阅：<br /><br /> -   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：参考](../modeling/layer-diagrams-reference.md)<br />-   [层关系图：准则](../modeling/layer-diagrams-guidelines.md)<br />-   [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|
|序列图|定义生命线的类型，并为生命线可接收的所有消息定义操作、参数和返回值。<br /><br /> 要根据类图上的某个类型创建生命线，请右键单击该类型，然后单击“创建生命线”。<br /><br /> 请参阅：<br /><br /> -   [UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)<br />-   [UML 序列图：准则](../modeling/uml-sequence-diagrams-guidelines.md)|
|代码图|可视化现有代码中的组织和关系。<br /><br /> 要标识类、类的关系和类的方法，请创建一个显示这些元素的代码图。<br /><br /> 请参阅：<br /><br /> -   [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)|

### <a name="DescribeLayers"></a>描述逻辑体系结构：层关系图
 层关系图通过将解决方案中的项目整理到抽象组或 *“层”* 来描述系统的逻辑体系结构。 项目可以为多种元素，如命名空间、项目、类、方法等。 层可表示和描述项目在系统中扮演的角色或执行的任务。 你也可以将层验证包含在生成和签入操作中，来确保代码与其设计保持一致。

 为了使代码和设计保持一致，Dinner Now 和 Lucerne 使用以下层关系图来验证相关代码：

 ![集成支付系统的层关系图](../modeling/media/layer-integrated-dnlucerne.png "Layer_Integrated_DNLucerne")

 **与 Lucerne 集成的晚餐的层关系图**

 此关系图上的层会链接到相应的 Dinner Now 和 Lucerne 解决方案项目。 例如，业务层会链接到 DinnerNow.Business 命名空间及其成员，该层现在包含 PaymentApprover 类。 资源访问层会链接到 DinnerNow.Data 命名空间。 箭头（即 *“依赖关系”* ）指定只有业务层可以使用资源访问层中的功能。 在团队更新其代码时，会定期执行层验证以便在发生冲突时进行捕获，并帮助团队快速解决冲突。

 两个团队密切合作，逐步集成并测试这两个系统。 他们在处理 PaymentProcessing 之前，会先确保 PaymentApprover 和 Dinner Now 的其他人员成功协作。

 下面的代码图显示了 Dinner Now 与 PaymentApprover 之间的新调用：

 ![通过集成系统更新了依赖项关系图](../modeling/media/depgraph-intsystem.png "DepGraph_IntSystem")

 **带有更新的方法调用的代码图**

 在确认系统按预期运行后，Dinner Now 会注释掉 PaymentProcessing 代码。 层验证报告未报告错误，生成的代码图显示没有其他 PaymentProcessing 依赖关系：

 ![不带 PaymentProcessing 的依赖项关系图](../modeling/media/depgraph-nomore.png "DepGraph_NoMore")

 **没有 PaymentProcessing 的代码图**

#### <a name="drawing-a-layer-diagram"></a>绘制层关系图
 层关系图具有以下主要功能：

- *“层”* ，描述项目的逻辑组。

- *“链接”* ，它是层和项目之间的关联。

   要根据项目创建层，请从解决方案资源管理器、代码图、类视图或对象浏览器中拖动项。 要绘制新层，然后将它们链接到项目，请使用工具箱或右键单击关系图图面以创建层，然后将项拖动到这些层。

   层上的数字显示链接到该层的项目数。 这些项目可以是命名空间、项目、类、方法等。 在解释层上的项目数时，请记住以下事项：

  - 如果某个层链接到一个包含其他项目的项目，但该层未直接链接到其他项目，则该数字仅包括链接的项目。 但是，在层验证过程中其他项目包括在分析范围内。

     例如，如果一个层链接到单个命名空间，则链接的项目数是 1，即使该命名空间包含类也是如此。 如果该层还链接到命名空间中的每个类，则该数字将包括链接的类。

  - 如果一个层包含链接到项目的其他层，则容器层也链接到这些项目，即使容器层上的数字不包括这些项目。

    要查看链接到某个层的项目，请右键单击该层，然后单击“查看链接” 以打开“层资源管理器”。

- *“依赖关系”* ，指示某个层可以使用另一个层中的功能，但反过来行不通。 *“双向依赖关系”* ，指示某个层可以使用另一个层中的功能，反之亦然。

   要显示层关系图上的现有依赖关系，请右键单击关系图图面，然后单击“生成依赖项”。 要描述预期的依赖关系，请绘制新的依赖关系。

  请参阅：

- [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)

- [层关系图：参考](../modeling/layer-diagrams-reference.md)

- [层关系图：指南](../modeling/layer-diagrams-guidelines.md)

- [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

#### <a name="summary-strengths-of-layer-diagrams"></a>摘要：层关系图的优点
 层关系图可帮助你：

- 根据系统项目的功能描述该系统的逻辑体系结构。

- 确保正在开发的代码与指定的设计保持一致。

#### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系

|**关系图**|**描述**|
|-----------------|---------------------|
|代码图|可视化现有代码中的组织和关系。<br /><br /> 要创建层，请生成一个代码图，然后将该代码图上的项作为可能的层进行分组。 将组从代码图拖动到层关系图。<br /><br /> 请参阅：<br /><br /> -   [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br />-   [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)|
|组件图|描述组件、组件的接口以及它们之间的关系。<br /><br /> 要可视化层，请创建一个描述系统中不同组件的功能的组件图。<br /><br /> 请参阅：<br /><br /> -   [UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)<br />-   [UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)|

## <a name="external-resources"></a>外部資源

|**类别**|**Links**|
|------------------|---------------|
|**论坛**|-   [Visual Studio 可视化和建模工具](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|

## <a name="see-also"></a>请参阅
 [可视化代码](../modeling/visualize-code.md)[为应用程序创建模型](../modeling/create-models-for-your-app.md)[在开发过程中使用模型](../modeling/use-models-in-your-development-process.md)在开发过程中[使用模型在](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f)[开发过程中验证系统](../modeling/validate-your-system-during-development.md)[扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
