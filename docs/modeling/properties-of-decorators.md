---
title: 修饰器的属性
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3374c07cac01104354b2ce41abddbeabbec0a373
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75566132"
---
# <a name="properties-of-decorators"></a>修饰器的属性
修饰器是可在关系图上的形状或连接线上出现的图标、文本或展开/折叠燕尾形。 下表显示了三种修饰器的属性。 某些属性仅出现在修饰器形状上，或仅出现在连接器修饰器上。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

## <a name="expandcollapse-decorator"></a>展开/折叠修饰器

|Property|描述|默认值|
|-|-|-|
|DisplayName|将在生成的设计器中显示的修饰器的名称。|展开折叠修饰器|
|Name|修饰器的名称。|ExpandCollapseDecorator|
|注释|与此修饰器关联的非正式注释。|\<none>|
|HorizontalOffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|VerticalOffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 （仅限连接器。）|0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 （仅限连接器。）|0|
|位置|修饰器的默认位置。|SourceTop|

## <a name="icon-decorator"></a>图标修饰器

|Property|描述|默认值|
|-|-|-|
|DefaultIcon|要显示的图标或图像文件的路径。|\<none>|
|DisplayName|要在生成的设计器中显示的修饰器的名称。|图标修饰器|
|Name|修饰器的名称。|IconDecorator|
|注释|与修饰器关联的非正式注释。|\<none>|
|HorizontalOffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|VerticalOffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 （仅限连接器。）|0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 （仅限连接器。）|0|
|位置|修饰器的默认位置。|SourceTop|

## <a name="textdecorator"></a>TextDecorator

|Property|描述|默认值|
|-|-|-|
|DefaultText|要显示的默认文本。|标签|
|DisplayName|要在生成的设计器中显示的修饰器的名称。|标签|
|FontSize|修饰器中所显示文本的字体大小。|8|
|FontStyle|修饰器中所显示文本的字体样式。|Regular|
|Name|修饰器的名称。|标签|
|注释|与修饰器关联的非正式注释。|\<none>|
|HorizontalOffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|VerticalOffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 （仅限连接器。）|0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 （仅限连接器。）|0|
|位置|修饰器的默认位置。|TargetBottom|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
