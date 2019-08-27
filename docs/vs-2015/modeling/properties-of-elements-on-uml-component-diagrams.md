---
title: UML 组件图上元素的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.componentdiagram.shapes.properties
helpviewer_keywords:
- component diagrams, properties
- UML, element properties
ms.assetid: fa0a9460-6675-4642-aa00-50f8719a892d
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c7f3f30d08fb62defec5e783da286e968a6b17c9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444427"
---
# <a name="properties-of-elements-on-uml-component-diagrams"></a>UML 组件图中元素的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 组件图中，图上的每个元素都具有属性。 若要查看某个元素的属性，请右键单击元素关系图上或在**UML 模型资源管理器**，然后单击**属性**。 属性将显示在**属性**窗口。  
  
> [!NOTE]
> 本主题主要讲述 UML 组件图中元素的属性。 有关如何读取 UML 组件图的详细信息，请参阅[UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)。 有关如何绘制 UML 组件图的详细信息，请参阅[UML 组件图：指导原则](../modeling/uml-component-diagrams-guidelines.md)。  
  
## <a name="properties-of-elements"></a>元素的属性  
  
|属性|默认|元素|描述|  
|--------------|-------------|-------------|-----------------|  
|**名称**|默认名称|全部|标识元素。|  
|**限定的名称**|Namespace::名称|全部|唯一标识元素。<br /><br /> 组件或类型的名称以包含该名称的包的限定名称为前缀。<br /><br /> 部件或端口的名称以拥有该名称的组件的限定名称为前缀。|  
|**工作项**|0 associated|全部|与此元素关联的工作项的数目。 若要将工作项相关联，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。|  
|**说明**|(无)|全部|可在此处记下有关元素的常规说明。|  
|**Color**|（该类型的默认值）|组件、部件、委派、部件程序集|形状的颜色。 与其他属性不同，这是形状的颜色，而不是形状所显示的模型元素的颜色。|  
|**为间接实例化**|True|组件|组件仅作为设计项目存在。 在运行时只有其部件存在。|  
|**是抽象的**|False|组件|组件定义只能用作泛化，可从中使其他组件特殊化。|  
|**可见性**|Public|组件、部件、端口|**公共**-全局可见。<br /><br /> **包**-在包内可见。<br /><br /> **专用**-在所属组件内可见。<br /><br /> **受保护的**-对派生自所有者的组件可见。|  
|**Type**|创建时的类型|部件<br /><br /> 端口|部件的类型为组件或类。<br /><br /> 端口的类型为接口。|  
|**重数**|1|部件<br /><br /> 端口|指示形成父组件的一部分的指定类型的实例的数量。<br /><br /> `1` - 恰好一个。<br /><br /> `0..1` - 一个或无。<br /><br /> `*` - 任意数量的集合。<br /><br /> `n..m` - 从 n 到 m 个实例的集合。|  
|**是行为**|False|端口|如果为 true，到此端口的消息由描述为组件的部件的活动或操作来处理，而不是由其部件处理。|  
|**是服务**|False|端口|如果为 true，则此端口是此组件的已发布接口的一部分。|  
|**LinkedPackage**|模型|关系图|添加到此关系图中的元素的默认命名空间。|  
  
## <a name="see-also"></a>请参阅  
 [UML 用例关系图：引用](../modeling/uml-use-case-diagrams-reference.md)   
 [UML 用例关系图：指南](../modeling/uml-use-case-diagrams-guidelines.md)
