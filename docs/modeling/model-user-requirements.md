---
title: 建立用户需求模型
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- requirements
- stories
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68aa46b3dc07813b73921b8acb5970289c30aecc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658415"
---
# <a name="model-user-requirements"></a>建立用户需求模型

通过绘制有关用户的活动和你的系统在帮助他们实现自己目标上所起到的作用的关系图，Visual Studio 可帮助你了解你的用户，并与他们展开讨论、沟通其要求。 需求模型是一组这样的关系图，每一张图都将重点放在用户需求的不同方面。 有关视频演示，请参阅： [业务域建模](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-3-modeling-the-business-domain)。

若要查看支持每种类型的模型的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

需求模型可帮助你：

- 将系统的外部行为与其内部设计区分开来进行重点关注。

- 与使用自然语言相比，在描述用户和利益相关者的需求方面产生的歧义更少。

- 定义可供用户、开发人员和测试人员使用的一致术语术语表。

- 减小要求的差距和不一致性。

- 减少对更改要求作出响应所需的工作量。

- 计划未来开发各种功能的顺序。

- 使用模型作为系统测试的基础，明确测试和要求之间的关系。 要求发生改变时，这种关系将帮助你正确地更新测试。 这可以确保系统满足新的要求。

如果在与用户或其代表进行重点讨论时使用需求模型，并在每次迭代开始时重新查看需求模型，那么使用需求模型会获得最大的好处。 无需在编写代码之前详细地完成它。 即使是非常简单的部分工作的应用程序，通常也能构成与用户讨论需求时的最具激励性的基础。 模型是汇总讨论结果的一种有效方式。 有关详细信息，请参阅[在开发过程中使用模型](../modeling/use-models-in-your-development-process.md)。

> [!NOTE]
> 在这些主题中，“系统”表示正在开发的系统或应用程序。 它可能是许多软件和硬件组件的大型集合、单个应用程序或一个更大型系统内的某个软件组件。 在每种情况下，需求模型都描述了在系统外部可以通过用户界面或 API 看到的行为。

## <a name="common-tasks"></a>常见任务

可以根据用户需求创建多个不同的视图。  每个视图都提供特定类型的信息。  在创建这些视图时，最好经常在视图间移动。 可以从任意视图开始。

|关系图或文档|需求模型中描述的内容|节|
|-|-|-|
|概念类图|用于描述要求的类型术语表；类型可以在系统界面中看到。||
|附加文档或工作项|性能、安全性、可用性和可靠性条件。|[描述服务质量要求](#QoSRequirements)|
|附加文档或工作项|不针对特定用例的约束和规则|[显示业务规则](#BusinessRules)|

请注意，大多数关系图类型可以用于其他目的。 有关关系图类型的概述，请参阅为[应用程序创建模型](../modeling/create-models-for-your-app.md)。

## <a name="BusinessRules"></a> Showing Business Rules

业务规则是一个不与特定用例相关联的要求，应在整个系统中进行观察。

许多业务规则受概念类间关系的约束。 您可以编写这些*静态业务规则*作为与概念类图上的相关类关联的注释。 例如:

![附加到 Order 类的注释中的规则。](../modeling/media/uml_reqmcd2.png)

*动态业务规则* 对允许的事件序列进行约束。 例如，使用序列或活动图来显示用户必须在登录后才能在你的系统上执行其他操作。

但是，许多动态规则都可以替换为静态规则，以便更高效、更泛地指定它们。 例如，你可以向概念类模型的类中添加一个 Boolean 属性“已登录”。 将“已登录”添加为登录用例的后置条件，并将其添加为大多数其他用例的前置条件。 这种方法可以让你避免对所有可能的事件序列组合进行定义。 这种方法在你需要向模型添加新用例时，也更加灵活。

请注意，此处的选择是有关你如何定义要求的方式，与你如何在程序代码中实现要求无关。

下列主题提供了更多信息：

|了解|读取|
|-|-|
|如何开发符合业务规则的代码|[应用体系结构建模](../modeling/model-your-app-s-architecture.md)|

## <a name="QoSRequirements"></a> Describing Quality of Service Requirements

服务质量要求有多个类别。 它们包括以下类型：

- 性能

- 安全

- 可用性

- 可靠性

- 稳定性

可以在特定用例的描述中包括其中的一些要求。 其他要求并不特定于用例，并已经非常高效地写入了单独文档。 如果可能，遵守要求模型定所定义的词汇非常有用。 在下面的示例中，请注意，要求中使用的主要词语是参与者、用例和上述插图中的类的标题：

如果餐厅在顾客订餐时删除了菜单项，则任何引用该菜单项的订单项将显示为红色。

有关如何开发符合服务质量要求的代码，请参阅为[应用程序的体系结构建模](../modeling/model-your-app-s-architecture.md)。

## <a name="see-also"></a>请参阅

- [在你的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)
- [应用体系结构建模](../modeling/model-your-app-s-architecture.md)
