---
title: 图像形状的属性
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.selectimagedialog
- vs.dsltools.dsldesigner.imageshape
helpviewer_keywords:
- Domain-Specific Language, image shape
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a89d7e5710f7a80c4e1f134ce2dfe2bd35ed5337
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658146"
---
# <a name="properties-of-image-shapes"></a>图像形状的属性

您可以使用 "图像形状" 来指定域类在生成的设计器中的显示方式。 通过将类的 `Image` 属性设置为预定义的图像文件来定义图像形状。 支持以下格式：

- .gif

- .jpg

- jpeg

- .bmp

- .wmf

- .emf

- .png

默认情况下，设计器资源文件（例如图像文件）位于**Dsl**项目的**Resources**文件夹中。

有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

图像形状具有下表中列出的属性。

|Property|描述|Default|
|-|-|-|
|填充颜色|此形状的填充颜色。|白色|
|填充渐变模式|此形状的填充渐变模式。|水平|
|具有默认连接点|如果 `True`，则该形状将使用生成的设计器中的顶部、底部、左侧和右侧连接点。|False|
|轮廓颜色|此形状的边框颜色。|黑色|
|空心虚线样式|此形状的边框虚线样式（纯色、划线、点、DashDot、DashDotDot 或自定义）。|单色|
|边框粗细|此形状的边框宽度。|0.03125|
|文本颜色|与此形状相关联的文本修饰器所使用的颜色。|黑色|
|访问修饰符|几何形状的访问修饰符（公共或内部）。|Public|
|自定义特性|用于将特性添加到从此形状生成的源代码类中。|\<none>|
|生成双派生|如果 `True`，则将生成基类和分部类（以支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|具有自定义构造函数|如果 `True`，将在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|继承修饰符|描述从图像形状（`none`、`abstract` 或 `sealed`）生成的源代码类的继承类型。|无|
|基本图像形状|此形状的基类。|(无)|
|“属性”|此形状的名称。|当前名称|
|Namespace|与此形状关联的命名空间。|当前命名空间|
|Tooltip 类型|定义工具提示的位置（"固定"、"变量" 或 "无"）。 如果已修复，则使用 `Fixed Tooltip Text` 属性的值作为工具提示;如果是变量，则在自定义代码中定义工具提示。|无|
|注意|与此形状相关联的非正式注释。|\<none>|
|初始高度|此形状的初始高度（英寸）。|1|
|初始宽度|此形状的初始宽度（英寸）。|1.5|
|作为属性公开的填充颜色<br /><br /> 公开的填充渐变模式<br /><br /> 作为属性公开的大纲颜色<br /><br /> 已公开大纲虚线样式为属性<br /><br /> 作为属性公开的大纲粗细<br /><br /> 公开文本颜色|如果 `True`，则用户可以设置形状的指定属性。 若要设置此项，请右键单击形状定义，然后单击 "添加" "**公开**"。|False|
|描述|用于记录生成的设计器。|\<none>|
|显示名称|将在生成的设计器中显示的此形状的名称。|\<none>|
|固定工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此元素的 F1 帮助的关键字。|\<none>|
|Image|用于此形状的图像文件的路径。|\<none>|

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)