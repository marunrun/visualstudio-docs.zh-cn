---
title: UML 组件图中元素的属性 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 39350a9e1d340651f8e15de109ecf61eb98996bb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671447"
---
# <a name="properties-of-elements-on-uml-component-diagrams"></a>UML 组件图中元素的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 组件图中，图上的每个元素都具有属性。 若要查看某个元素的属性，请在关系图或 " **UML 模型资源管理器**" 中右键单击该元素，然后单击 "**属性**"。 属性将显示在 "**属性**" 窗口中。

> [!NOTE]
> 本主题主要讲述 UML 组件图中元素的属性。 有关如何读取 UML 组件图的详细信息，请参阅[Uml 组件图：参考](../modeling/uml-component-diagrams-reference.md)。 有关如何绘制 UML 组件图的详细信息，请参阅[Uml 组件图：准则](../modeling/uml-component-diagrams-guidelines.md)。

## <a name="properties-of-elements"></a>元素的属性

|Property|Default|元素|描述|
|--------------|-------------|-------------|-----------------|
|**名称**|默认名称|全部|标识元素。|
|**限定名称**|命名空间 :: 名称|全部|唯一标识元素。<br /><br /> 组件或类型的名称以包含该名称的包的限定名称为前缀。<br /><br /> 部件或端口的名称以拥有该名称的组件的限定名称为前缀。|
|**工作项**|0 associated|全部|与此元素关联的工作项的数目。 若要关联工作项，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。|
|**描述**|(无)|全部|可在此处记下有关元素的常规说明。|
|**颜色**|（该类型的默认值）|组件、部件、委派、部件程序集|形状的颜色。 与其他属性不同，这是形状的颜色，而不是形状所显示的模型元素的颜色。|
|**间接实例化**|True|组件|组件仅作为设计项目存在。 在运行时只有其部件存在。|
|**是抽象的**|False|组件|组件定义只能用作泛化，可从中使其他组件特殊化。|
|**可见性**|Public|组件、部件、端口|**公共**-全局可见。<br /><br /> **包-在**包中可见。<br /><br /> **Private** -在所属组件中可见。<br /><br /> **Protected** -对派生自所有者的组件可见。|
|**Type**|创建时的类型|部件<br /><br /> 端口|部件的类型为组件或类。<br /><br /> 端口的类型为接口。|
|**多样性**|1|部件<br /><br /> 端口|指示形成父组件的一部分的指定类型的实例的数量。<br /><br /> `1` - 恰好一个。<br /><br /> `0..1` - 一个或无。<br /><br /> `*` - 任意数量的集合。<br /><br /> `n..m` - 从 n 到 m 个实例的集合。|
|**是行为**|False|端口|如果为 true，到此端口的消息由描述为组件的部件的活动或操作来处理，而不是由其部件处理。|
|**Is 服务**|False|端口|如果为 true，则此端口是此组件的已发布接口的一部分。|
|**LinkedPackage**|型号|关系图|添加到此关系图中的元素的默认命名空间。|

## <a name="see-also"></a>请参阅
 [Uml 用例图：引用](../modeling/uml-use-case-diagrams-reference.md) [uml 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)
