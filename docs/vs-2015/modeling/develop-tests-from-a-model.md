---
title: 从模型开发测试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- tests and requirements
ms.assetid: 40f87192-ba85-4552-8804-314a678261ae
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2b9fec6954706fcecb1281650a8db3d85f08fbd0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669788"
---
# <a name="develop-tests-from-a-model"></a>基于模型开发测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用要求模型和体系结构模型来帮助组织系统及其组件的测试。 这种做法有助于确保你测试了对于用户和其他利益干系人而言非常重要的要求，并可帮助你在要求发生变化时快速更新测试。 如果你使用 [!INCLUDE[TCMext](../includes/tcmext-md.md)]，还可以维护模型和测试之间的链接。

 若要查看支持这些功能的 Visual Studio 版本，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="system-and-subsystem-testing"></a>系统和子系统测试
 *系统测试*也称为*验收测试*，这意味着测试是否满足用户的需求。 这种测试关注系统的外部可见行为，而不是内部设计。

 在扩展或重新设计系统时，系统测试非常有价值。 它们将帮助你避免在更改代码时引入 bug。

 在计划对系统进行任何更改或扩展时，从一组在现有系统上运行的测试开始着手会很有帮助。 然后，你可以对测试进行扩展或调整以测试新的要求，对代码进行更改，以及重新运行全套测试。

 开发新系统时，你可以在开始进行开发时着手创建测试。 通过在开发每项功能前定义测试，你可以用非常特定的方式来捕获要求讨论。

 子系统测试对系统的主要组件应用相同的原则。 每个组件都与其他组件分开进行测试。 子系统测试的重点是在组件的用户界面或 API 中可见的行为。

 有关如何运行测试的详细信息，请参阅[测试应用程序](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)。

## <a name="deriving-system-tests-from-a-requirements-model"></a>从需求模型派生系统测试
 你可以创建并维护系统测试和需求模型之间的关系。 若要建立这种关系，你可以编写对应需求模型主要元素的测试。 Visual Studio 通过允许你在测试和模型的各个部件之间创建链接，帮助你维护这一关系。 有关要求模型的详细信息，请参阅[模型用户需求](../modeling/model-user-requirements.md)。

### <a name="write-tests-for-each-use-case"></a>为每个用例编写测试
 如果你使用 [!INCLUDE[TCMext](../includes/tcmext-md.md)]，则可以为你在要求模型中定义的每个用例创建一组测试。 例如，如果你有一个“订餐”用例，其中包括“创建订单”和“向订单添加项”，则你可以为这些用例的整体和细节创建测试。 有关用例的详细信息，请参阅[UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)。

 这些准则可能会有所帮助：

- 每个用例应具有多个测试，用于获得主要路径和异常结果。

- 描述需求模型中的用例时，与详细描述用户为实现目标需遵循的过程相比，定义用例的后置条件（即实现的目标）更重要。 例如，“订餐”的后置条件可以是餐馆正在为顾客准备餐点和顾客已付款。 后置条件是测试应验证的条件。

- 使单独测试基于后置条件的单独子句。 例如，创建单独测试以在有订单时通知餐馆并向顾客收取款项。 此分离具有这些好处：

  - 需求的不同方面通常独立发生更改。 按这种方法将测试分成不同方面，可以在需求发生更改时更方便地更新测试。

  - 如果开发计划逐个实现用例的方面，则你可以随着开发的进展单独启用测试。

- 设计测试时，请将测试数据的选择与确定是否已实现后置条件的代码或脚本分离。 例如，一个简单算术函数的测试可能为：输入 4；验证输出为 2。 实际上，将脚本设计为：选择一个输入；将其本身乘以输出，然后验证结果为原始输入。 此样式允许你在不更改测试主体的情况下改变测试输入。

#### <a name="linking-tests-to-use-cases"></a>将测试链接到用例
 如果使用 [!INCLUDE[TCMlong](../includes/tcmlong-md.md)] 来设计和运行测试，则可以在 "要求"、"用例" 或 "用户情景" 工作项下组织测试。 你可以将这些工作项链接到模型中的用例。 这样你便可以快速跟踪测试的需求更改，并有助于你跟踪每个用例的进度。

###### <a name="to-link-tests-to-a-use-case"></a>将测试链接到用例

1. 在 [!INCLUDE[TCMlong](../includes/tcmlong-md.md)] 中，创建一个要 求并使测试套件基于该需求。 若要了解如何执行此操作，请参阅[测试应用程序](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)。

    所创建的要求是 [!INCLUDE[vstsTfsShort](../includes/vststfsshort-md.md)] 中的工作项。 它可以是用户情景、要求或用例工作项，具体取决于项目在 [!INCLUDE[esprfound](../includes/esprfound-md.md)] 中使用的过程模板。 有关详细信息，请参阅[使用 Visual Studio Team Services 或 Team Foundation Server 跟踪工作](https://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)。

2. 将要求工作项链接到模型中的一个或多个用例。

    在用例图中，右键单击用例，然后单击 "**链接到工作项**"。 有关详细信息，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。

3. 添加到测试套件（即验证用例的测试用例）。

   通常，每个用户情景或要求工作项将链接到模型中的多个用例，且每个用例将链接到多个用户情景或要求。 这是因为，每个用户情景或需求包括一组开发多个用例的任务。 例如，你可以在项目的早期迭代中开发基本用户情景，客户可以从用户情景的目录中选择项并进行提交。 在后期迭代中，情景可以是用户在完成订单时支付的款项以及供应商在发送货物后收到的金额。  每个情景都向“订货”用例的后置条件中添加一个子句。

   可以将后置条件的子句写入用例图上的单独注释，从而创建从要求到这些子句的单独链接。 可以将每个注释链接到要求工作项，并将注释链接到关系图上的用例。

### <a name="base-tests-on-the-requirements-types"></a>使测试基于要求类型
 需求模型的类型（即类、接口和枚举）依据用户对其业务的考虑和传达方式来描述概念和关系。 不包括仅与系统的内部设计有关的类型。

 根据这些需求类型设计你的测试。 这种做法有助于确保在讨论需求更改时，可以容易地将这些更改与测试中的必要更改相关。 这样，能够与最终用户和其他利益干系人直接讨论测试及其预期结果。 这意味着可以在开发过程外部维护用户的需求，并避免无意中围绕设计中的可能缺陷设计测试。

 对于手动测试，此做法包括遵循测试脚本中的需求模型的词汇。 对于自动测试，此做法包括使用需求类图作为测试代码的基础，以及创建取值函数和 updater 函数以将需求模型链接到代码。

 例如，要求模型可能包括“菜单”、“菜单项”、“订单”类型以及这些类型之间的关联。 虽然此模型表示由订餐系统存储和处理的信息，但不表示实现该信息的复杂性。 在工作系统中，数据库、用户界面和 API 中的每个类型都可能有数种不同的实现。 在分布式系统中，每个实例的多种变体可能同时存储在系统的不同部件中。

 若要测试用例（例如“添加订单项”），测试方法可能包括类似下面的代码：

```
Order order = … ; // set up an order
// Store prior state:
int countBefore = order.MenuItems.Count;
// Perform use case:
MenuItem chosenItem = …; // choose an item
AddItemToOrder (chosenItem, order);
// Verify part of postcondition:
int countAfter = order.MenuItems.Count;
Assert (countAfter == countBefore = 1);
```

 请注意，此测试方法使用要求模型的类。 关联和特性作为 .NET 属性实现。

 若要实现此目的，必须将类的属性定义为只读函数或取值函数，这些函数访问系统以检索有关其当前状态的信息。 模拟用例的方法（例如 AddItemToOrder）必须通过其 API 或通过其用户界面下的层驱动系统。 测试对象（例如订单和菜单项）的构造函数也必须驱动系统，以在系统内部创建相应项。

 可以通过应用程序的正常 API 使用多个取值函数和 updater。 但是可能需要编写一些附加函数才能启用测试。 这些附加取值函数和 updater 有时称为“测试检测”。 由于这些函数依赖于系统的内部设计，因此，系统开发人员的职责就是提供这些函数，而测试人员则根据求模型编写测试代码。

 编写自动测试时，可以使用一般测试来包装取值函数和 updater。 有关详细信息，请参阅[创建使用一般测试运行可执行文件的自动测试](https://msdn.microsoft.com/library/b8dadaf4-4473-49c5-a0d9-46eca9e65d52)。

### <a name="tests-for-business-rules"></a>业务规则的测试
 某些需求不与任何一个用例直接相关。 例如，DinnerNow 业务允许顾客从多个菜单中选择，但要求每个订单中所有选择的项都应来自一个菜单。 可以将此业务规则表示为有关在求类模型中的订单、菜单和项之间的关联的固定规则。

 此类型的固定规则不仅控制当前定义的所有用例，而且控制将在以后定义的任何其他用例 因此，独立于任何用例编写此规则并独立于用例单独进行测试非常有用。

 可以编写固定业务规则作为类图中的注释。 有关详细信息，请参阅[UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)。

 通过将注释链接到要求或用户情景工作项（可将该工作项链接到 [!INCLUDE[TCMlong](../includes/tcmlong-md.md)] 中的测试套件），可以将测试链接到业务规则。 有关详细信息，请参阅[将测试用例附加到模型元素](#Attaching)。

 可以在用例图、活动图或序列图的注释中说明性能和其他服务质量要求。 你也可以将这些注释链接到需求工作项及其测试套件。

### <a name="sequence-and-activity-diagrams-for-tests"></a>测试序列图和活动图
 如果需求模型或体系结构模型包括序列图或活动图，则你可以编写直接遵守这些关系图的测试。

 设计这样的测试有时很有用：通过关系图中的分支和循环动态选择不同路径。

 尝试在验证每个消息或操作之后验证系统的状态。 这可能需要进行其他检测。

## <a name="deriving-subsystem-tests-from-models"></a>从模型派生子系统测试
 在大型系统的高级设计中，可以标识组件或子系统。 这些表示可以单独设计、或位于不同计算机上或者是可通过多种方式重新组合的可重用模块的部件。 有关详细信息，请参阅[UML 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)。

 你可以对每个主要组件与完整系统应用相同的原则。 在大型项目中，每个组件都可以具有其自己的需求模型。 在较小的项目中，可以创建体系结构模型或高级设计以显示主要组件及其交互。 有关详细信息，请参阅为[应用程序的体系结构建模](../modeling/model-your-app-s-architecture.md)。

 在任何情况下，你都可以按照将在需求模型和系统测试之间建立关系的相同方式，在模型元素和子系统测试之间建立一种关系。

### <a name="isolate-components-with-provided-and-required-interfaces"></a>使用提供的接口和所需的接口隔离各个组件
 标识组件对系统的其他部件或外部服务具有的所有依赖项，并将这些依赖项表示为所需的接口非常有用。 此练习通常导致需要重新进行某些设计，这可使组件更易于分离，且可以与设计的其余部分轻松分离。

 此分离的一个优点是，可以通过将 mock 对象替换为组件通常使用的服务来执行组件以进行测试。 这些组件是为实现测试目的而设置的组件。 mock 组件提供你的组件所需的接口，以响应使用模拟数据的查询。 mock 组件构成完整测试工具的部件，你可以将测试工具连接到组件的所有接口。

 mock 测试的优点是你可以在自己的组件将使用其服务的其他组件仍在开发时，开发自己的组件。

## <a name="maintain-the-relationships-between-tests-and-model"></a>维护测试和模型之间的关系
 在每隔几周执行一次迭代的典型项目中，在每次迭代快开始时都要检查需求。 会议讨论将在下一次迭代中提交的功能。 可以使用需求模型帮助讨论概念、方案和将要开发的操作序列。 业务利益干系人设置优先级，开发人员进行估算，测试人员确保正确实现每项功能的预期行为。

 编写测试是定义需求的最有效方法，也是确保人员明确所需内容的有效方法。 但是，虽然在具体研讨会期间需要很长时间才能编写测试，但是可以更快速地创建模型。

 从测试的角度来看，可以将需求模型看做是测试的简略形式。 因此，在整个项目中维护测试和模型之间的关系非常重要。

## <a name="Attaching"></a>将测试用例附加到模型元素
 如果你的项目使用 [!INCLUDE[TCMlong](../includes/tcmlong-md.md)]，则你可以将测试链接到模型中的元素。 这样你便可以快速找到受要求中的更改影响的测试，并且可帮助你跟踪要求的实现程度。

 你可以将测试链接到所有类型的元素。 下面是一些可能的恶意活动：

- 将用例链接到执行它的测试。

- 在链接到用例的注释上编写用例后置条件或目标的子句，然后将测试链接到每个注释。

- 在类图或活动图上的注释中编写固定规则，然后将这些注释链接到测试。

- 将测试链接到活动图或单个活动。

- 将测试套件链接到它测试的组件或子系统。

#### <a name="to-link-tests-to-a-model-element-or-relationship"></a>将测试链接到模型元素或关系

1. 在 [!INCLUDE[TCMlong](../includes/tcmlong-md.md)] 中，创建一个要 求并使测试套件基于该需求。 若要了解如何执行此操作，请参阅[测试应用程序](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)。

     所创建的要求是 [!INCLUDE[vstsTfsShort](../includes/vststfsshort-md.md)] 中的工作项。 它可以是用户情景、要求或用例工作项，具体取决于项目在 [!INCLUDE[esprfound](../includes/esprfound-md.md)] 中使用的过程模板。 有关详细信息，请参阅[使用 Visual Studio Team Services 或 Team Foundation Server 跟踪工作](https://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)。

2. 将要求工作项链接到模型中的一个或多个元素。

     在建模图中，右键单击元素、注释或关系，然后单击 "**链接到工作项**"。 有关详细信息，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。

3. 添加到测试套件（即验证模型元素中表示的需求的测试用例）。

## <a name="see-also"></a>请参阅
 [为应用模型创建模型](../modeling/create-models-for-your-app.md)[用户需求](../modeling/model-user-requirements.md)[模型应用体系结构](../modeling/model-your-app-s-architecture.md)[分析和建模体系结构](../modeling/analyze-and-model-your-architecture.md)
