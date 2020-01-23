---
title: 关于域特定语言
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bfd073b07902e3c0a9e33dfe9ae50d4947a50ef2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597264"
---
# <a name="about-domain-specific-languages"></a>关于域特定语言

与一般用途语言（如C#或 UML）不同，域特定语言（DSL）设计为在特定的问题空间或域中表示语句。

众所周知的 Dsl 包括正则表达式和 SQL。 每个 DSL 比用于描述文本字符串或数据库操作的通用语言好得多，但对于描述在其自身范围之外的观点更糟。 各个行业也有其自己的 Dsl。 例如，在电信行业中，呼叫描述语言广泛用于指定电话呼叫中的状态序列，在空中旅行行业，使用标准 DSL 描述航班预订。

你的业务和你的项目还将处理可通过 DSL 描述的特殊概念集。 例如，可以为以下应用程序之一定义 DSL：

- 规划网站中的导航路径。

- 电子组件的接线图。

- 用于传送带的传送带和行李处理设备的网络。

设计 DSL 时，为域中的每个重要概念定义*域类*，如网页、灯具或机场检入办公桌。 您可以定义*域关系*，如超链接、线路或传送带，以将概念链接在一起。

DSL 的用户创建*模型。* 模型是 DSL 的*实例*。 例如，它们描述特定的网站、特定设备的布线或特定机场中的行李处理系统。

用户可以将模型作为关系图或 Windows 窗体查看。 还可以将模型视为 XML，这是存储这些模型的方式。 定义 DSL 时，可以定义每个域类和关系的实例在用户屏幕上的显示方式。 典型 DSL 显示为通过箭头连接的图标或矩形的集合。

下图显示了关系图 DSL 中的小型模型：

![都铎王朝家谱模型](../modeling/media/tudor_familytreemodel.png)

## <a name="what-you-can-do-with-dsls"></a>可以通过 Dsl 执行的操作

DSL 的典型应用是生成程序代码或其他项目。 定义 DSL 时，可以定义用于读取 DSL 型号并生成文本文件的*文本模板*。

例如，你可以编写采用机场计划的模板并生成用于行李处理的部分软件，以及描述该计划的部分用户文档。

定义 DSL 后，可以将其分发给可以在自己的计算机上安装它的其他用户。 DSL 的用户可在 Visual Studio 中创建和编辑模型。

你还可以定义菜单命令和其他工具，这些工具可帮助用户编辑 DSL、验证约束以帮助确保正确使用 DSL，以及帮助用户创建新实例的项模板。 可以将一个或多个 Dsl 连同其工具和其他 Visual Studio 扩展作为集成包进行包装。

通常，当开发团队必须为多个产品编写类似的代码时，就会创建域特定语言。 例如，一家专门从事行李处理系统的公司可能会定义一个行李轨迹 DSL，他们可以在其中生成每个安装的某些代码。 DSL 的优点在于，它可以由其客户理解，而从该系统生成的代码则可靠，并且如果客户的需求改变，系统就可以快速更新。

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使你能够创建一个具有自己的图形设计器和自己的关系图表示法的域特定语言，然后使用该语言为每个项目生成相应的源代码。

## <a name="domain-specific-development"></a>特定于域的开发

特定于域的开发是一种过程，该过程通过使用域特定语言，然后构造语言并将其部署到应用程序开发人员来确定可建模的部分应用程序。 开发人员使用域特定语言来构造特定于其应用程序的模型，使用这些模型生成源代码，然后使用源代码来开发应用程序。

## <a name="aspects-of-graphical-domain-specific-development"></a>图形域特定开发的各个方面

图形域特定语言必须包含以下功能：

- Notation

- 域模型

- 项目生成

- Serialization

- 与 Visual Studio 的集成

### <a name="notation"></a>Notation

域特定语言必须具有一组合理的元素，这些元素可以很容易地定义和扩展以表示特定于域的构造。 表示法由图形组成，表示元素和连接线，它们表示图形图面上元素之间的关系。 在 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]中，可以对形状进行扩展和优化，以表示域特定语言的元素。

### <a name="domain-model"></a>域模型

域特定语言必须将元素集和它们之间的关系组合到一个一致的语法中。 它还必须定义元素和关系的组合是否有效。 例如，编程语言通常会阻止循环继承，其中一个类派生自另一个类，第二个类派生自第一个类。 约束还可用于表示业务逻辑，例如，一个人不能是自己的依赖项。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使用约束来表达大多数特定于域的语言所需的限制类型。

### <a name="artifact-generation"></a>项目生成

域特定语言的主要用途之一就是生成一个项目，例如源代码、XML 文件或其他一些可用的数据。 通常情况下，模型中的更改表示项目中的更改。 您可以使用 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 来生成项目，并在更改模型时重新生成项目。

### <a name="serialization"></a>Serialization

必须以某种形式保留域特定语言，以便进行编辑、保存、关闭和重新加载。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使用 XML 格式，该格式允许定义和自定义如何序列化或保存域特定语言。

### <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成

由于 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 是在 Visual Studio 中承载的，因此它扩展了许多 Visual Studio 窗口和控件。 它还允许您自定义菜单命令、工具箱项和用户界面的其他元素的行为。

你还可以为特定于域的语言创建模型总线适配器。 此适配器允许您引用模型中的模型和元素，并使您可以编写可访问和更新 DSL 实例的代码。 使用强大的模型总线机制，可以编写适用于多个模型的 Visual Studio 扩展。 你还可以编写适用于模型的独立应用程序。 有关详细信息，请参阅[使用 Visual Studio 集成模型 Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。

## <a name="benefits-of-domain-specific-development"></a>域特定开发的优点

域特定语言可以提供以下优点：

- 包含完全适合于问题空间的构造。

     与通用语言不同，域特定语言由直接表示问题空间逻辑的元素和关系组成。 例如，保险政策应用程序必须包含策略和声明的元素。 通过域特定语言，可更轻松地设计应用程序，并查找和更正逻辑错误。

- 允许非开发人员和不知道域的人员了解总体设计。

     通过使用图形域特定语言，可以创建域的可视化表示形式，以便非开发人员可以轻松地了解应用程序的设计。

- 可以更方便地创建最终应用程序的原型。

     开发人员可以使用其模型生成的代码来创建可显示给客户端的原型应用程序。

## <a name="the-process-of-domain-specific-development"></a>域特定开发过程

使用域特定语言的大多数软件开发团队按照以下步骤创建并使用其模型：

- 团队将域的可变部分与从不更改的部件区分开来。

- 开发人员为固定部分编写代码，并为变量部分保留扩展点。

- 领导软件开发人员或架构师创建了一种特定于域的语言，该语言包含域固定部分的设计模式和可变部分的扩展点。

- 领导软件开发人员或架构师将域特定语言部署到团队生成的各种应用程序的开发人员。

- 每个开发人员创建一个适用于特定应用程序的模型。
