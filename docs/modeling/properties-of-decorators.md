---
title: 修饰器的属性
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 76129141ed293281eeb3179a654f470bcf608bdf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62996795"
---
# <a name="properties-of-decorators"></a>修饰器的属性
修饰器是图标、 文本或展开/折叠尖括号中显示的形状或关系图上的连接器。 下表显示三种类型的修饰器的属性。 某些属性会显示仅在形状修饰器或仅连接器修饰器。

 有关详细信息，请参阅[如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

## <a name="expandcollapse-decorator"></a>展开/折叠修饰器

|属性|描述|默认|
|-|-|-|
|DisplayName|修饰器将生成的设计器中显示的名称。|展开折叠修饰器|
|名称|修饰器的名称。|ExpandCollapseDecorator|
|说明|与此修饰器相关联的非正式说明。|\<none>|
|HorizontalOffset|水平偏移量，相对于修饰器，以英寸为单位的默认位置。 （在形状上仅。）|0|
|VerticalOffset|垂直偏移量，相对于修饰器，以英寸为单位的默认位置。 （在形状上仅。）|0|
|OffsetFromLine|修饰器在行中，相对于其默认位置，以英寸为单位的偏移量。 （有关连接器仅。）|0|
|OffsetFromShape|修饰器从相应的形状，相对于其默认位置，以英寸为单位的偏移量。 （有关连接器仅。）|0|
|位置|修饰器默认位置。|SourceTop|

## <a name="icon-decorator"></a>图标修饰器

|属性|描述|默认|
|-|-|-|
|DefaultIcon|要显示的图标或图像文件的路径。|\<none>|
|DisplayName|修饰器要在生成的设计器中显示的名称。|图标修饰器|
|名称|修饰器的名称。|IconDecorator|
|说明|与修饰器相关联的非正式说明。|\<none>|
|HorizontalOffset|水平偏移量，相对于修饰器，以英寸为单位的默认位置。 （在形状上仅。）|0|
|VerticalOffset|垂直偏移量，相对于修饰器，以英寸为单位的默认位置。 （在形状上仅。）|0|
|OffsetFromLine|修饰器在行中，相对于其默认位置，以英寸为单位的偏移量。 （有关连接器仅。）|0|
|OffsetFromShape|修饰器从相应的形状，相对于其默认位置，以英寸为单位的偏移量。 （有关连接器仅。）|0|
|位置|修饰器默认位置。|SourceTop|

## <a name="textdecorator"></a>TextDecorator

|属性|描述|默认|
|-|-|-|
|DefaultText|要显示的默认文本。|Label|
|DisplayName|修饰器要在生成的设计器中显示的名称。|Label|
|FontSize|修饰器中显示的文本的字体大小。|8|
|FontStyle|修饰器中显示的文本的字体样式。|规则|
|名称|修饰器的名称。|Label|
|说明|与修饰器相关联的非正式说明。|\<none>|
|HorizontalOffset|水平偏移量，相对于修饰器，以英寸为单位的默认位置。 （在形状上仅。）|0|
|VerticalOffset|垂直偏移量，相对于修饰器，以英寸为单位的默认位置。 （在形状上仅。）|0|
|OffsetFromLine|修饰器在行中，相对于其默认位置，以英寸为单位的偏移量。 （有关连接器仅。）|0|
|OffsetFromShape|修饰器从相应的形状，相对于其默认位置，以英寸为单位的偏移量。 （有关连接器仅。）|0|
|位置|修饰器默认位置。|TargetBottom|

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)