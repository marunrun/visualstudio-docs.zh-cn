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
ms.openlocfilehash: 14965f829530ba5a2f6a7797291e9d1cfab0ae2d
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810049"
---
# <a name="properties-of-decorators"></a>修饰器的属性
修饰器是可在关系图上的形状或连接线上出现的图标、文本或展开/折叠燕尾形。 下表显示了三种修饰器的属性。 某些属性仅出现在修饰器形状上，或仅出现在连接器修饰器上。

 有关详细信息，请参阅 [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅 [自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

## <a name="expandcollapse-decorator"></a>展开/折叠修饰器

|Property|说明|默认|
|-|-|-|
|DisplayName|将在生成的设计器中显示的修饰器的名称。|展开折叠修饰器|
|“属性”|修饰器的名称。|ExpandCollapseDecorator|
|注释|与此修饰器关联的非正式注释。|\<none>|
|System.windows.controls.primitives.popup.horizontaloffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 仅对形状 (。 ) |0|
|System.windows.controls.primitives.popup.verticaloffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 仅对形状 (。 ) |0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 仅对连接器 (。 ) |0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 仅对连接器 (。 ) |0|
|位置|修饰器的默认位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.sourcetop|

## <a name="icon-decorator"></a>图标修饰器

|Property|说明|默认|
|-|-|-|
|DefaultIcon|要显示的图标或图像文件的路径。|\<none>|
|DisplayName|要在生成的设计器中显示的修饰器的名称。|图标修饰器|
|“属性”|修饰器的名称。|IconDecorator|
|注释|与修饰器关联的非正式注释。|\<none>|
|System.windows.controls.primitives.popup.horizontaloffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 仅对形状 (。 ) |0|
|System.windows.controls.primitives.popup.verticaloffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 仅对形状 (。 ) |0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 仅对连接器 (。 ) |0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 仅对连接器 (。 ) |0|
|位置|修饰器的默认位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.sourcetop|

## <a name="textdecorator"></a>TextDecorator

|Property|说明|默认|
|-|-|-|
|DefaultText|要显示的默认文本。|Label|
|DisplayName|要在生成的设计器中显示的修饰器的名称。|Label|
|FontSize|修饰器中所显示文本的字体大小。|8|
|FontStyle|修饰器中所显示文本的字体样式。|定期|
|“属性”|修饰器的名称。|Label|
|注释|与修饰器关联的非正式注释。|\<none>|
|System.windows.controls.primitives.popup.horizontaloffset|相对于修饰器默认位置的水平偏移量（以英寸为单位）。 仅对形状 (。 ) |0|
|System.windows.controls.primitives.popup.verticaloffset|相对于修饰器默认位置的垂直偏移量（以英寸为单位）。 仅对形状 (。 ) |0|
|OffsetFromLine|从行修饰器的偏移量（以英寸为单位），相对于其默认位置。 仅对连接器 (。 ) |0|
|OffsetFromShape|修饰器相对于其默认位置的偏移量（以英寸为单位）。 仅对连接器 (。 ) |0|
|位置|修饰器的默认位置。|Microsoft.visualstudio.modeling.diagrams.connectordecoratorposition.targetbottom|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))