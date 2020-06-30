---
title: 分段形状的属性
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.compartmentshape
helpviewer_keywords:
- Domain-Specific Language, compartment shape
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 51b652adcc482d6e326c0b64eda3a9d32efab309
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532284"
---
# <a name="properties-of-compartment-shapes"></a>分段形状的属性
隔离舱形状是可用于在域特定语言中显示域类的一种形状。 您可以展开和折叠隔离舱。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 隔离舱形状具有下表中列出的属性。

|properties|说明|默认|
|-|-|-|
|默认展开折叠状态|如果 `Expanded` 为，则在创建时显示隔离舱。 如果 `Collapsed` 为，则不是。|展开|
|填充颜色|此形状的填充颜色。|白色|
|填充渐变模式|此形状的填充渐变模式。|横向|
|Geometry|此形状的几何图形（矩形或圆角矩形）。|矩形|
|具有默认连接点|如果为 `True` ，则形状将使用生成的设计器中的顶部、底部、左侧和右侧连接点。|False|
|单个隔离舱标题可见|如果 `False` 为，且形状具有单个隔离舱，则隔离舱的标头将不可见。|True|
|轮廓颜色|此形状的边框颜色。|黑色|
|空心虚线样式|此形状的边框虚线样式（纯色、破折号、点、DashDot、DashDotDot、Custom）。|单色|
|边框粗细|此形状的边框宽度。|0.03125|
|文本颜色|与此形状相关联的文本修饰器的颜色。|黑色|
|访问修饰符|隔离舱形状（或）的访问级别 `public` `internal` 。|公共|
|自定义特性|用于向此隔离舱形状生成的源代码类添加特性|\<none>|
|生成双派生|如果为 `True` ，则将生成基类和分部类（以支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|具有自定义构造函数|如果为 `True` ，则在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|继承修饰符|描述从隔离舱形状（或）生成的源代码类的继承类型 `none` `abstract` `sealed` 。|无|
|基本隔离舱形状|此形状的基类。|（无）|
|名称|此形状的名称。|当前名称|
|命名空间|与此形状关联的命名空间。|当前命名空间|
|Tooltip 类型|如何定义工具提示（"固定"、"变量" 或 "无"）。 如果已修复，则属性的值 `Fixed Tooltip Text` 将用作工具提示; 如果变量为，则在自定义代码中定义工具提示。|none|
|注意|与此形状相关联的非正式注释。|\<none>|
|初始高度|此形状的初始高度（英寸）。 对于隔离舱形状，这只是标头部分的高度，无法调整其大小。|1|
|初始宽度|此形状的初始宽度（英寸）。|1.5|
|作为属性公开的填充颜色<br /><br /> 公开的填充渐变模式<br /><br /> 作为属性公开的大纲颜色<br /><br /> 已公开大纲虚线样式为属性<br /><br /> 作为属性公开的大纲粗细<br /><br /> 公开文本颜色|如果 `True` 为，则用户可以设置形状的指定属性。 若要设置此项，请右键单击形状定义，然后单击 "添加" "**公开**"。|False|
|说明|用于记录生成的设计器。|\<none>|
|显示名称|将在生成的设计器中显示的此形状的名称。|\<none>|
|固定工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此形状的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)