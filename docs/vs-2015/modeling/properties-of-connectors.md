---
title: 连接器的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, connectors
ms.assetid: b1f24e8d-cdd7-4a5d-af37-1038f43b45c7
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1ea629e504c3ba74d35f3ad8aa89bc22cfae30df
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652039"
---
# <a name="properties-of-connectors"></a>连接线的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

连接器表示生成的设计器中的域关系。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 连接器具有下表中列出的属性。

|Property|描述|Default|
|--------------|-----------------|-------------|
|颜色|此连接符的颜色。|黑色|
|虚线样式|此连接符线的虚线样式（纯色、破折号、点、DashDot、DashDotDot 或 Custom）。|单色|
|源结束样式|此连接器的源端样式（Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.hollowarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptyarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filledarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptydiamond、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filleddiamond 或 None）。|None|
|目标结束样式|此连接符的目标端样式（Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.hollowarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptyarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filledarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptydiamond、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filleddiamond 或 None）。|None|
|文本颜色|与此连接器关联的文本修饰器所使用的颜色。|黑色|
|Thickness|此连接符线的粗细（英寸）。|0.03125|
|访问修饰符|类的访问级别（`public` 或 `internal`）。|Public|
|自定义特性|用于向从此连接器生成的源代码类添加特性。|\<none>|
|生成双派生|如果 `True`，则将生成基类和分部类（以支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|具有自定义构造函数|如果 `True`，将在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|继承修饰符|描述从连接器（`none`、`abstract` 或 `sealed`）生成的源代码类的继承类型。|无|
|基本连接器|此连接器的基类。|(无)|
|“属性”|此连接器的名称。|当前名称|
|Namespace|与此连接器关联的命名空间。|当前命名空间|
|Tooltip 类型|如何定义工具提示（"固定"、"变量" 或 "无"）。 如果已修复，则使用 `Fixed Tooltip Text` 属性的值作为工具提示;如果是变量，则在自定义代码中定义工具提示。|\<none>|
|注意|与此连接器关联的非正式注释。|\<none>|
|路由样式|用于路由连接器的样式。 @No__t_0 连接器会按需向右倾斜;不 `Straight` 连接器。|折线|
|作为属性公开的颜色<br /><br /> 已公开虚线样式为属性<br /><br /> 以属性形式显示粗细<br /><br /> 公开文本颜色|如果 `True`，则用户可以设置形状的指定属性。 若要设置此项，请右键单击形状定义，然后单击 "添加" "**公开**"。|False|
|描述|用于记录生成的设计器。|\<none>|
|显示名称|将在生成的设计器中显示的此连接器的名称。|\<none>|
|固定工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此元素的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>请参阅
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
