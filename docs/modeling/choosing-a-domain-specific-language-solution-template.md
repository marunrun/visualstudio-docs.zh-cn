---
title: 选择域特定语言解决方案模板
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, solution templates
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6b3e6d9812f06df6d4af65f624579ec5f6550515
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62424058"
---
# <a name="choosing-a-domain-specific-language-solution-template"></a>选择域特定语言解决方案模板
若要创建域特定语言解决方案，请选择一个特定于域的语言设计器向导中提供的解决方案模板。 通过选择最近似你想要创建的语言的模板，可以尽量减少您必须对起始解决方案进行的修改。

 域特定语言设计器向导中提供了以下解决方案模板。

|模板|功能|描述|
|-|-|-|
|类图|-隔离舱形状<br />类继承<br />关系继承<br />形状继承<br />-关系属性|如果您的特定于域的语言包括实体和关系具有属性，请使用此解决方案模板。 此模板创建类似于 UML 类图的特定于域的语言。 三大要素是类和接口，以及关联、 泛化和实现关系。 类或接口显示为一个包含属性的列表框。|
|组件图|-端口|如果您的特定于域的语言包括组件，即，软件系统的部分，请使用此解决方案模板。 此模板创建类似于 UML 组件图的特定于域的语言。 三大要素是组件和端口，则显示为小形状外侧的组件。|
|任务流关系图|-图像和几何形状<br />-   *泳道*|如果您的特定于域的语言包括工作流、 状态或序列，请使用此解决方案模板。 此模板创建类似于 UML 活动图的特定于域的语言。 主实体是一项活动，并且主要关系是活动之间的转换。 该模板包含多个其他元素，如启动状态，最终状态，并同步栏。|
|最小语言|-一个类和形状<br />-一个关系和连接器|如果您的特定于域的语言不像其他模板，请使用此解决方案模板。 此模板创建具有两个类和一个关系，以表示特定于域的语言**工具箱**作为**框中**并**行**。 类和关系都有一个示例字符串属性。|
|最小 WinForm 设计器|-A 小型模型。<br />-Windows 窗体中显示该模型。|如果你想要生成应用程序中 DSL 绑定到 Windows 窗体，而不是图形设计器，请使用此模板。<br /><br /> 充当该语言的用户界面的窗体是 Dsl\UI 的文件夹中。<br /><br /> 打开窗体设计器之前，应先生成项目。<br /><br /> 有关详细信息，请参阅[创建 Windows Forms-Based 域特定语言](../modeling/creating-a-windows-forms-based-domain-specific-language.md)。|
|最小 WPF 设计器|-A 小型模型<br />的显示模型一个 Windows Presentation Foundation 用户界面|如果你想要生成应用程序中 DSL 绑定到 WPF 用户界面，而不是图形设计器，请使用此模板。<br /><br /> 用户界面的设计器处于文件夹 Dsl\UI。<br /><br /> 打开 UI 设计器之前，应先生成项目。<br /><br /> 有关详细信息，请参阅[创建 WPF-Based 域特定语言](../modeling/creating-a-wpf-based-domain-specific-language.md)。|
|DSL 库|-最小的库|如果你想要生成可以导入到其他 DSL 定义的部分 DSL 定义，请使用此模板。|

## <a name="see-also"></a>请参阅

- [域特定语言工具的概述](../modeling/overview-of-domain-specific-language-tools.md)
