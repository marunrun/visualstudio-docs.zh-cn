---
title: 关于域特定语言
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4684a0256e01cafe79fc90ae1ae97dfc2be047d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823357"
---
# <a name="about-domain-specific-languages"></a>关于域特定语言

与常规用途语言如 C# 或 UML，不同域特定语言 (DSL) 被用于 express 的特定问题空间或域中的语句。

熟知的 Dsl 包括正则表达式和 SQL。 每个 DSL 是大大优于通用语言用于描述文本字符串或数据库，但差很多操作来描述其自己的作用域外的想法。 各个行业也有其自己的 Dsl。 例如，在电信行业中，调用的说明语言都广泛使用电话呼叫，在指定状态的序列，并且在无线移动行业的标准 DSL 用于描述航班预订。

你的业务和你的项目还处理特殊组无法与 DSL 所述的概念。 例如，可以定义一个这些应用程序的 DSL:

- 在网站中的导航路径的计划。

- 电子组件的绑定关系图。

- 传送带和行李处理设备的机场的网络。

在设计 DSL 时，您定义*域类*为每个域，如网页、 lamp 或机场签入服务台中的重要概念。 您定义*域关系*如超链接、 网络或传送带将概念连接在一起。

你的 DSL 的用户创建*模型。* 模型是*实例*的 DSL。 例如，它们描述特定网站或特定设备或行李处理系统中特定机场的绑定。

作为关系图或 Windows 窗体，用户可以查看模型。 模型可以还查看作为 XML 使用，这是存储方式。 定义 DSL 时，您定义的每个域类和关系实例在用户屏幕上的显示方式。 典型的 DSL 显示为图标或矩形由箭头连接的集合。

下图显示在关系图 DSL 的小型模型：

![都铎王朝家谱模型](../modeling/media/tudor_familytreemodel.png)

## <a name="what-you-can-do-with-dsls"></a>您可以使用 Dsl 做什么

DSL 的典型的应用程序是生成程序代码或其他项目。 在定义 DSL 时，可以定义*文本模板*，读取 DSL 模型并生成文本文件。

例如，可以编写可采用的机场计划并生成的软件的行李处理，以及一些的用户文档说明了在计划的一部分的模板。

定义 DSL 后，可以将其分发给其他用户可以在自己的计算机上安装它。 你的 DSL 的用户可以创建和编辑 Visual Studio 中的模型。

您还可以定义菜单命令和其他工具，可帮助用户编辑 DSL，验证约束，以帮助我们确保 DSL 的使用正确无误，并帮助用户项模板创建新的实例。 为集成包，可以包装其工具和其他 Visual Studio 扩展的一个或多个 Dsl。

通常情况下，当开发团队必须编写类似的代码的多个产品创建特定于域的语言。 例如，一家专门从事行李处理系统的公司可能会定义从中它们可能会产生一些的代码对于每个安装的行李跟踪 DSL。 DSL 的优点是，您可以了解其客户从其生成的代码是可靠的并且，系统可以快速更新如果客户的要求发生更改。

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 可以创建具有自己的图形设计器和你自己的关系图表示法，特定于域的语言，然后使用该语言生成相应的源代码中，为每个项目。

## <a name="domain-specific-development"></a>特定于域的开发

特定于域的开发是标识的应用程序使用特定于域的语言，然后构造语言并将其部署到应用程序开发人员可以建模部分的过程。 开发人员使用特定于域的语言来构建模型，这是特定于其应用程序，使用模型来生成源代码，并使用的源代码来开发应用程序。

## <a name="aspects-of-graphical-domain-specific-development"></a>图形的特定于域的开发方面

图形的特定于域的语言必须包括以下功能：

- Notation

- 域模型

- 项目生成

- 序列化

- 与 Visual Studio 的集成

### <a name="notation"></a>Notation

特定于域的语言必须具有相当一小组可轻松地定义和扩展来表示特定于域的构造的元素。 表示法由形状表示的元素和连接器，它表示元素，请在图形关系图图面之间的关系组成。 在[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]，可以扩展的形状，并将其优化来表示特定于域的语言的元素。

### <a name="domain-model"></a>域模型

特定于域的语言必须组合元素和它们到一致的语法之间的关系集。 它还必须定义组合的元素和关系是否有效。 例如，编程语言通常禁止循环继承，在其中从第二个类派生一个类和第二个类派生自的第一个类。 此外可以使用约束来表达业务逻辑，例如，一个人不能为自己的依赖项。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使用约束来表示类型的最特定于域的语言要求的限制。

### <a name="artifact-generation"></a>项目生成

域特定语言的主要用途之一是生成项目，例如，源代码、 XML 文件或一些其他可用的数据。 通常情况下，模型中的更改意味着在项目中的更改。 可以使用[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]以生成项目并重新生成此类模型更改时。

### <a name="serialization"></a>序列化

必须以某种形式的可编辑、 保存、 关闭并重新加载保留特定于域的语言。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使用 XML 格式，可用于定义和自定义序列化或保持特定于域的语言如何。

### <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成

因为[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]托管在 Visual Studio 中，它扩展了很多 Visual Studio 窗口和控件。 它还允许您自定义菜单命令、 工具箱项和其他元素的用户界面的行为。

此外可以为特定于域的语言创建模型总线适配器。 此适配器允许你引用模型和模型，并允许您编写代码，可以访问和更新 DSL 的实例中的元素。 通过使用功能强大的模型总线机制，可以编写多个模型的 Visual Studio 扩展。 此外可以编写适用于模型的独立应用程序。 有关详细信息，请参阅[通过使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。

## <a name="benefits-of-domain-specific-development"></a>特定于域的开发的好处

域特定语言可提供以下优势：

- 包含完全适应问题空间的构造。

     不同于常规用途语言，域特定语言包含元素和直接表示问题空间的逻辑关系。 例如，保险策略应用程序必须包括有关策略和声明的元素。 域特定语言，可以更轻松地设计应用程序，并查找和更正错误的逻辑。

- 允许非开发人员和其他人不知道了解整体设计的域。

     通过使用图形的特定于域的语言，可以创建的域的可视表示形式，以便非开发人员可以轻松地了解应用程序的设计。

- 可以更轻松地创建最终的应用程序的原型。

     开发人员可以使用它们的模型生成创建原型应用程序，它们可显示给客户端的代码。

## <a name="the-process-of-domain-specific-development"></a>特定于域的开发过程

使用域特定语言的大多数软件开发团队按照以下步骤来创建和使用其模型：

- 团队将永远不会更改的部分从域的变量部分区分开来。

- 开发人员编写代码的固定部分，并保留的变量部分的扩展点。

- 首席软件开发人员或架构师创建一种特定于域的语言，其中包含域和变量部分的扩展点的固定部分的设计模式。

- 首席软件开发人员或架构师团队生成的各种应用程序的开发人员到部署域特定语言。

- 每个开发人员创建适用于特定应用程序的模型。