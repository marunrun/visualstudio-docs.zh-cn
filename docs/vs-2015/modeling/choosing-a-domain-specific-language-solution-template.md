---
title: 选择域特定语言解决方案模板 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, solution templates
ms.assetid: 9c05955f-1548-4df6-b09b-4b348823c237
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 36b821219b02fa77171d89214d8cf4813ce92303
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433389"
---
# <a name="choosing-a-domain-specific-language-solution-template"></a>选择域特定语言解决方案模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要创建域特定语言解决方案，请选择一个特定于域的语言设计器向导中提供的解决方案模板。 通过选择最近似你想要创建的语言的模板，可以尽量减少您必须对起始解决方案进行的修改。  
  
 域特定语言设计器向导中提供了以下解决方案模板。  
  
> [!NOTE]
> 模板的用途是提供起始 DSL。 名为类和组件图的模板不是完整的 UML 关系图。 如果你想要创建 UML 模型，请考虑 UML 建模工具，提供了一组围绕单个模型集成的关系图。 这些关系图是可扩展的，并且可以使用 ModelBus 与你的 DSL 集成。 有关详细信息，请参阅[为您的应用程序创建模型](../modeling/create-models-for-your-app.md)。  
  
|模板|功能|描述|  
|--------------|--------------|-----------------|  
|类图|-隔离舱形状<br />类继承<br />关系继承<br />形状继承<br />-关系属性|如果您的特定于域的语言包括实体和关系具有属性，请使用此解决方案模板。 此模板创建类似于 UML 类图的特定于域的语言。 三大要素是类和接口，以及关联、 泛化和实现关系。 类或接口显示为一个包含属性的列表框。|  
|组件图|-端口|如果您的特定于域的语言包括组件，即，软件系统的部分，请使用此解决方案模板。 此模板创建类似于 UML 组件图的特定于域的语言。 三大要素是组件和端口，则显示为小形状外侧的组件。|  
|任务流关系图|-图像和几何形状<br />-   *泳道*|如果您的特定于域的语言包括工作流、 状态或序列，请使用此解决方案模板。 此模板创建类似于 UML 活动图的特定于域的语言。 主实体是一项活动，并且主要关系是活动之间的转换。 该模板包含多个其他元素，如启动状态，最终状态，并同步栏。|  
|最小语言|-一个类和形状<br />-一个关系和连接器|如果您的特定于域的语言不像其他模板，请使用此解决方案模板。 此模板创建具有两个类和一个关系，以表示特定于域的语言**工具箱**作为**框中**并**行**。 类和关系都有一个示例字符串属性。|  
|最小 WinForm 设计器|-A 小型模型。<br />-Windows 窗体中显示该模型。|如果你想要生成应用程序中 DSL 绑定到 Windows 窗体，而不是图形设计器，请使用此模板。<br /><br /> 充当该语言的用户界面的窗体是 Dsl\UI 的文件夹中。<br /><br /> 打开窗体设计器之前，应先生成项目。<br /><br /> 有关详细信息，请参阅[创建 Windows Forms-Based 域特定语言](../modeling/creating-a-windows-forms-based-domain-specific-language.md)。|  
|最小 WPF 设计器|-A 小型模型<br />的显示模型一个 Windows Presentation Foundation 用户界面|如果你想要生成应用程序中 DSL 绑定到 WPF 用户界面，而不是图形设计器，请使用此模板。<br /><br /> 用户界面的设计器处于文件夹 Dsl\UI。<br /><br /> 打开 UI 设计器之前，应先生成项目。<br /><br /> 有关详细信息，请参阅[创建 WPF-Based 域特定语言](../modeling/creating-a-wpf-based-domain-specific-language.md)。|  
|DSL 库|-最小的库|如果你想要生成可以导入到其他 DSL 定义的部分 DSL 定义，请使用此模板。|  
  
## <a name="see-also"></a>请参阅  
 [域特定语言工具的概述](../modeling/overview-of-domain-specific-language-tools.md)
