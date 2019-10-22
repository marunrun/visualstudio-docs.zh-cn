---
title: 关系图的属性
ms.date: 10/31/2018
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 73be8223d661617451d548898164b78a1a1563f0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658227"
---
# <a name="properties-of-diagrams"></a>关系图的属性
您可以设置属性，以指定关系图在生成的设计器中的显示方式。 例如，可以在关系图中指定文本的默认颜色。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 下表列出了关系图的属性。

|Property|描述|Default|
|-|-|-|
|填充颜色|关系图的填充颜色。|白色|
|文本颜色|显示在关系图上的文本的颜色。|黑色|
|访问修饰符|类的访问修饰符（公共或内部）。|Public|
|自定义特性|用于将特性添加到生成的代码类。|\<none>|
|生成双派生|如果 `True`，则将生成基类和分部类（以支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|具有自定义构造函数|如果 `True`，将在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|继承修饰符|描述从关系图（`none`、`abstract` 或 `sealed`）生成的源代码类的继承类型。|None|
|基本关系图|此关系图的基类。|(无)|
|“属性”|此关系图的名称。|当前名称|
|Namespace|与此关系图关联的命名空间。|当前命名空间|
|表示的类|此关系图表示的根域类。|当前根类（如果适用）|
|注意|与此元素相关联的非正式注释。|\<none>|
|将填充颜色作为属性公开|如果 `True`，则用户可以设置生成的设计器的关系图的填充颜色。 若要设置此属性，请右键单击关系图形状，然后单击 "添加" "**公开**"。|False|
|以属性形式显示文本颜色|如果 `True`，则用户可以在生成的设计器中设置关系图的文本颜色。 若要设置此属性，请右键单击关系图形状，然后单击 "添加" "**公开**"。|False|
|描述|用于记录生成的设计器的说明。|\<none>|
|显示名称|将在此关系图的生成的设计器中显示的名称。|\<none>|
|帮助关键字|用于索引此关系图的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>请参阅

[域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
