---
title: 连接器属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, connectors
ms.assetid: b1f24e8d-cdd7-4a5d-af37-1038f43b45c7
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a3673a818f9460b8b40bb3fee2dcd5fe65fd02a8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701734"
---
# <a name="properties-of-connectors"></a>连接线的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

连接符表示生成的设计器中的域关系。  
  
 有关详细信息，请参阅[如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。  
  
 连接器具有下表中列出的属性。  
  
|属性|描述|默认|  
|--------------|-----------------|-------------|  
|颜色|此连接符的颜色。|黑色|  
|短划线样式|此连接器 （纯色、 短划线、 圆点、 DashDot、 DashDotDot 或自定义） 的线条的短划线样式。|单色|  
|源端样式|（HollowArrow、 EmptyArrow、 FilledArrow、 EmptyDiamond、 FilledDiamond，或无） 此连接符源端样式。|None|  
|目标端样式|（HollowArrow、 EmptyArrow、 FilledArrow、 EmptyDiamond、 FilledDiamond，或无） 此连接符目标端样式。|None|  
|文本颜色|使用此连接器与相关联的文本修饰器的颜色。|黑色|  
|Thickness|此连接符线的粗细以英寸为单位测量。|0.03125|  
|访问修饰符|类的访问级别 (`public`或`internal`)。|Public|  
|自定义特性|用于将属性添加到此连接器从生成的源代码类。|\<none>|  
|生成双派生|如果`True`，将生成的基类和一个分部类 （以支持通过重写自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|  
|具有自定义构造函数|如果`True`，将在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|  
|继承修饰符|说明可从连接器生成的源代码类继承的类型 (`none`，`abstract`或`sealed`)。|无|  
|基本连接符|此连接器的基类。|(无)|  
|名称|此连接器的名称。|当前名称|  
|命名空间|隶属于此连接器命名空间。|当前命名空间|  
|工具提示类型|如何定义工具提示 （固定的变量，或无）。 如果固定，然后的值`Fixed Tooltip Text`属性用作工具提示; 如果变量，然后在工具提示中定义自定义代码。|\<none>|  
|说明|此连接器与相关联的非正式说明。|\<none>|  
|路由样式|为路由连接器使用的样式。 一个`Rectilinear`连接器可根据需要; 直角将`Straight`连接器不执行。|折线|  
|作为属性公开的颜色<br /><br /> 作为属性公开的短划线样式<br /><br /> 作为属性公开的粗细<br /><br /> 公开文本颜色|如果`True`，用户可以设置形状的规定的属性。 若要将此项设置，请右键单击形状定义，然后单击**公开添加**。|False|  
|描述|用于记录生成的设计器。|\<none>|  
|显示名称|将此连接器生成的设计器中显示的名称。|\<none>|  
|固定工具提示文本|用于固定工具提示文本。|\<none>|  
|帮助关键字|用于索引此元素的 F1 帮助关键字。|\<none>|  
  
## <a name="see-also"></a>请参阅  
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
