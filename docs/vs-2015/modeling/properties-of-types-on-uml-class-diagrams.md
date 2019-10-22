---
title: UML 类图上类型的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.logicalclassdiagram.shapes.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: 6e1ef2d0-d67a-401a-bd64-d5e034decd2c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9881393e792cf8bf49dc6d0b9459b18969dea171
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671322"
---
# <a name="properties-of-types-on-uml-class-diagrams"></a>UML 类图上类型的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 类图中，*类型*是类、接口或枚举。

> [!NOTE]
> 本主题介绍 UML 类图中的类型的属性。 有关更多信息，请参见下列主题：

- [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)

- [UML 类图：准则](../modeling/uml-class-diagrams-guidelines.md)

- [UML 类图上特性的属性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML 类图中操作的属性](../modeling/properties-of-operations-on-uml-class-diagrams.md)

- [UML 类图上关联的属性](../modeling/properties-of-associations-on-uml-class-diagrams.md)

## <a name="properties"></a>属性
 这些是类、接口或枚举的属性。

 若要查看某个类型的属性，请在关系图或**UML 模型资源管理器**中右键单击该类型，然后单击 "**属性**"。 属性将显示在 "**属性**" 窗口中。

|**Property**|**Default**|显示范围|描述|
|------------------|-----------------|----------------|-----------------|
|**名称**|默认名称|所有元素|标识元素。|
|**限定名称**|所含包 :: 类型名称|所有元素|唯一标识元素。 以包含它的包的限定名为前缀。|
|**颜色**|类型种类的默认值|所有元素|此形状的颜色。 与其他属性不同，这不是基础模型元素的属性。 相同类型的不同视图可以具有不同的颜色。|
|**是抽象的**|False|实例|如果为 true，则无法实例化类，且类旨在用作基类。|
|**为叶**|False|类、接口|如果为 true，则类型不需要具有派生类型。|
|**处于活动状态**|False|实例|如果为 true，则此类型的每个实例都与控制线程关联。|
|**可见性**|Public|类、接口、枚举|-Public-全局可见。<br />-Private-此类型在拥有它的包中可见。<br />-包-在包中可见。|
|**工作项**|0 associated|所有元素|与此元素关联的工作项的数目。 若要关联工作项，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。|
|**描述**|(空白)|所有元素|可在此处记下有关项的常规说明。|
|**模板绑定**|(无)|类、接口、枚举|如果不为空，则通过将参数值绑定到此模板类来定义该类型。 展开该属性可查看模板参数的绑定。|
|**模板参数**|(无)|类、接口、枚举|如果不为空，则为在此处列出参数的模板类。 若要添加参数或查看单个参数的属性，请单击 " **[...]** "。|

## <a name="see-also"></a>请参阅
 [Uml 类图上特性的](../modeling/properties-of-attributes-on-uml-class-diagrams.md)属性 uml 类图上[的操作](../modeling/properties-of-operations-on-uml-class-diagrams.md)的属性 uml 类图上的[关联的](../modeling/properties-of-associations-on-uml-class-diagrams.md)属性 uml 类图[：准则](../modeling/uml-class-diagrams-guidelines.md)
