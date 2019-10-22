---
title: 修饰器的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
ms.assetid: f6322fe5-dc08-4d32-a6b3-0bd18879136d
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cb837c9b3d465d229f64fac08dac02af8d50f5fa
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652009"
---
# <a name="properties-of-decorators"></a>修饰器的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

修饰器是可在关系图上的形状或连接线上出现的图标、文本或展开/折叠燕尾形。 下表显示了三种修饰器的属性。 某些属性仅出现在修饰器形状上，或仅出现在连接器修饰器上。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

## <a name="expandcollapse-decorator"></a>展开/折叠修饰器

|Property|描述|Default|
|--------------|-----------------|-------------|
|DisplayName|将在生成的设计器中显示的修饰器的名称。|展开折叠修饰器|
|“属性”|修饰器的名称。|ExpandCollapseDecorator|
|注意|与此修饰器关联的非正式注释。|\<none>|
|System.windows.controls.primitives.popup.horizontaloffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|System.windows.controls.primitives.popup.verticaloffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 （仅限连接器。）|0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 （仅限连接器。）|0|
|位置|修饰器的默认位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.sourcetop|

## <a name="icon-decorator"></a>图标修饰器

|Property|描述|Default|
|--------------|-----------------|-------------|
|DefaultIcon|要显示的图标或图像文件的路径。|\<none>|
|DisplayName|要在生成的设计器中显示的修饰器的名称。|图标修饰器|
|“属性”|修饰器的名称。|IconDecorator|
|注意|与修饰器关联的非正式注释。|\<none>|
|System.windows.controls.primitives.popup.horizontaloffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|System.windows.controls.primitives.popup.verticaloffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 （仅限连接器。）|0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 （仅限连接器。）|0|
|位置|修饰器的默认位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.sourcetop|

## <a name="textdecorator"></a>TextDecorator

|Property|描述|Default|
|--------------|-----------------|-------------|
|DefaultText|要显示的默认文本。|Label|
|DisplayName|要在生成的设计器中显示的修饰器的名称。|Label|
|FontSize|修饰器中所显示文本的字体大小。|8|
|FontStyle|修饰器中所显示文本的字体样式。|规则|
|“属性”|修饰器的名称。|Label|
|注意|与修饰器关联的非正式注释。|\<none>|
|System.windows.controls.primitives.popup.horizontaloffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|System.windows.controls.primitives.popup.verticaloffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 （仅适用于形状。）|0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 （仅限连接器。）|0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 （仅限连接器。）|0|
|位置|修饰器的默认位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.targetbottom|

## <a name="see-also"></a>请参阅
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
