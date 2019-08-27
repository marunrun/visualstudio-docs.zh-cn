---
title: 序列图中的 uml 元素的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.sequencediagram.combinedfragment.properties
- vs.teamarch.sequencediagram.shapes.properties
helpviewer_keywords:
- UML sequence diagrams, properties
- sequence diagrams, properties
ms.assetid: 475c10f3-a2d2-4a1e-b366-dc28997d437e
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a6008566f71a241fb5daccab8d6a5dcb68882452
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444396"
---
# <a name="properties-of-elements-on-uml-sequence-diagrams"></a>UML 序列图中元素的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 序列图中，关系图上的每个元素都具有属性。 若要查看某个元素的属性，请右键单击元素关系图上或在**UML 模型资源管理器**，然后单击**属性**。 属性将显示在**属性**窗口。  
  
> [!NOTE]
> 本主题关于 UML 序列图中元素的属性。 有关如何读取 UML 序列图的详细信息，请参阅[UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)。 有关如何绘制 UML 序列图的详细信息，请参阅[UML 序列图：指导原则](../modeling/uml-sequence-diagrams-guidelines.md)。  
  
## <a name="properties-of-elements"></a>元素的属性  
  
|属性|默认|元素|描述|  
|--------------|-------------|-------------|-----------------|  
|**名称**|默认名称|全部|标识元素。|  
|**限定的名称**|包::名称|全部|唯一标识元素。 以包含它的包的限定名为前缀。|  
|**工作项**|0 associated|全部|与此元素关联的工作项的数目。 若要将工作项相关联，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。|  
|**说明**|(空白)|全部|可在此处记下有关项的常规说明。|  
|**Color**|（元素类型的默认值）|生命线、消息|形状的颜色。 这是形状的属性而不是形状显示的元素。|  
|**Type**|(空白)|生命线|生命线表示的实例的类型。<br /><br /> 如果生命线的标头中显示有引用符号，则此类或接口在 UML 模型资源管理器中单独存在，并且可以显示在类图上。|  
|**Actor**|False|生命线|指示生命线表示的是用户、设备，还是该关系图所针对的组件外部的软件组件。|  
|**Kind**|**完整**-具有发送方和接收的消息。<br /><br /> **找到**-具有未指定发送方的消息。<br /><br /> **丢失**-具有未指定接收方的消息。|消息|指示将消息的哪一端附加到生命线。<br /><br /> 此属性无法更改。 在你创建消息时进行设置。|  
|**Sort**|**AsynchCall** -异步消息。<br /><br /> **SynchCall** -同步消息。<br /><br /> **回复**-同步消息的返回部分。<br /><br /> **CreateMessage** -实例创建消息。|消息|消息的类型。 此属性无法更改。 由用来创建消息的工具确定。|  
|**Operation**|（空）|消息|接收生命线中的消息所调用的方法。<br /><br /> 仅当接收生命线链接到接口或类时才可见。|  
|**是指**|序列图|交互使用|由此交互使用调用的序列图。|  
|**交互运算符**|在使用时设置**Surround With**命令|组合片段|此片段或片段集合表示的运算符。|  
|**防护**|（空）|组合片段中的交互操作数|除非“保护”为 True，否则片段中的序列将不会显示。<br /><br /> 若要选择任何组合片段的顶级片段，请在片段标题下面单击。|  
|**Min, Max**|（无限制）|循环组合片段|执行循环的最少次数和最大次数。|  
|**消息**|（空）|考虑和<br /><br /> 忽略组合片段|在此片段中考虑或忽略的消息。|  
  
## <a name="see-also"></a>请参阅  
 [UML 序列关系图：引用](../modeling/uml-sequence-diagrams-reference.md)   
 [UML 序列关系图：指导原则](../modeling/uml-sequence-diagrams-guidelines.md)   
 [使用 UML 序列图中的片段描述控制流](../modeling/describe-control-flow-with-fragments-on-uml-sequence-diagrams.md)
