---
title: UML 序列图：引用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.sequencediagram.diagram
- vs.teamarch.UMLModelExplorer.sequencediagram
- vs.teamarch.sequencediagram.toolbox
helpviewer_keywords:
- diagrams - modeling, sequence
- sequence diagrams
- UML diagrams, sequence
- diagrams - modeling, UML sequence
- UML, sequence diagrams
ms.assetid: 366fc324-aeeb-4894-bd13-ec2e40754b8e
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7f9b02bbad4fa897404f6c20e12b1705a3ae9ac8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661718"
---
# <a name="uml-sequence-diagrams-reference"></a>UML 序列图：参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，*序列图*显示了一个交互，表示类、组件、子系统或参与者的实例之间的消息序列。 时间流向图表下方，它显示从一个参与者到另一个参与者的控制流。 使用序列图来可视化实例和事件，而不是类和方法。 同一类型的多个实例可以出现在该关系图上。 同一条消息也会多次出现。

 UML 序列图是 UML 模型的一部分，并且仅存在于 UML 建模项目中。 若要创建 UML 序列图，请在 "**体系结构**" 菜单上单击 "**新建 UML 或层关系图**"。 了解有关如何创建和绘制[uml 序列图](../modeling/uml-sequence-diagrams-guidelines.md)或[uml 建模图](../modeling/edit-uml-models-and-diagrams.md)的详细信息。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="reading-sequence-diagrams"></a>读取序列图
 下表介绍了你可以在序列图上看到的元素。 了解有关这些[元素的属性](../modeling/properties-of-elements-on-uml-sequence-diagrams.md)的详细信息。

 ![序列图的各个部分](../modeling/media/uml-sequence.png "UML_Sequence")

|**整形**|**元素**|**描述**|
|---------------|-----------------|---------------------|
|1|**生命线**|竖线表示交互期间参与者中发生的事件序列，而时间发展沿此线向下。 此参与者可以是类、组件或参与者的实例。|
|2|**演员**|你开发的系统之外的参与者。<br /><br /> 您可以通过设置执行**组件的执行组件属性，** 使其显示在生命线的顶部。|
|3|**同步消息**|在它继续之前，发件人将等待同步消息响应。 图表同时显示了调用和返回。 同步消息用于表示程序中普通函数调用，并以相同方式表示其他种类消息的行为。|
|4|**异步消息**|在发件人继续之前无需响应的消息。 异步消息仅显示来自发件人的调用 用于表示单独的线程之间的通信或新线程的创建。|
|5|**执行发生次数**|带有阴影的垂直矩形显示在参与者的生命线上并表示参与者执行操作的时间段。<br /><br /> 执行开始时参与者会收到一条消息。 如果初始消息是一个同步消息，则执行以一个返回给发件人的 «返回» 箭头结束。|
|6|**回叫消息**|返回到等待之前调用返回的参与者的消息。 结果执行匹配项将出现在现有匹配项的顶部。|
|7|**自助消息**|消息从参与者传送到其本身。 结果执行匹配项将出现在发送执行的顶部。|
|8|**创建消息**|创建参与者的消息。 如果参与者收到一个创建消息，则该消息应该使其接收到的第一个消息。|
|9|**找到的消息**|来自未知或未指定参与者的异步消息。|
|10|**丢失消息**|向未知或未指定参与者发送的异步消息|
|11|**注释**|可以将注释附加到生命线上的任意点。|
|12|**交互使用**|包含在另一个关系图中定义的消息的序列。<br /><br /> 若要创建**交互使用**，请单击该工具，然后在要包括的生命线上拖动。|
|13|**组合片段**|片断的集合。 每个片段可以包含一个或多个消息。 组合片段有不同种类。 有关详细信息，请参阅[通过 UML 序列图上的片段描述控制流](../modeling/describe-control-flow-with-fragments-on-uml-sequence-diagrams.md)。<br /><br /> 若要创建片段，请右键单击消息，指向 "**外侧代码**"，然后单击片段类型。|
|14|**片段临界**|可用于表明与是否出现片段相关的条件。<br /><br /> 若要设置临界，请选择一个片段，然后选择该临界并键入一个值。|
|**X**|**析构事件**|表示对象被删除或不再可访问的点。 显示在每个生命线底部。|
||**交换**|在序列图中显示的邮件和生命线的集合。 若要查看交互的属性，必须在 " **UML 模型资源管理器**" 中选择它。|
||**序列图**|用于显示交互的关系图。 若要查看其属性，请单击关系图的空白部分。 **注意：** 序列图的名称、显示的交互以及包含关系图的文件都可以不同。|

## <a name="see-also"></a>请参阅
 [Uml 序列图：准则](../modeling/uml-sequence-diagrams-guidelines.md)[编辑 uml 模型和关系图](../modeling/edit-uml-models-and-diagrams.md) [UML 用例图：引用](../modeling/uml-use-case-diagrams-reference.md)Uml[类图](../modeling/uml-class-diagrams-reference.md)：引用 uml[组件图](../modeling/uml-component-diagrams-reference.md)：引用 uml[组件图](../modeling/uml-component-diagrams-reference.md)：引用
