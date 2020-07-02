---
title: 域角色的属性
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6c1c62126d65107bb25e3c4a475a794116c47193
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544139"
---
# <a name="properties-of-domain-roles"></a>域角色的属性
下表中的属性与域角色关联。 有关域角色的信息，请参阅[了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|Property|描述|默认|
|-|-|-|
|集合类型|如果此角色的多重性为 0 .. * 或 1 .. \* ，此属性将自定义用于存储链接集合的泛型类型。|`(none)` - <xref:Microsoft.VisualStudio.Modeling.LinkedElementCollection%601>使用|
|自定义特性|此处指定的特性将作为特性添加到生成的代码类中。|无 <\>|
|可浏览属性|如果 `True` 为，并且关系的重数为 0 ..1 或 1 ..1，则用户可以在 "**属性**" 窗口中浏览 role 属性。 属性显示关系链接另一端的元素的名称。|`True`|
|为属性生成器|如果 `True` 为，则生成此角色的角色属性，你可以使用该属性遍历程序代码中的关系。 如果将此项设置为 false，则可以通过使用域关系的静态方法以效率较低的方式遍历关系。|`True`|
|属性 Getter 访问修饰符|所生成属性的 getter 的访问修饰符（ `public` 、、、 `internal` `private` `protected` 或 `protected internal` ）。|`public`|
|属性 Setter 访问修饰符|生成的属性（ `public` 、 `internal` 、 `private` 、 `protected` 或 `protected internal` ）的 setter 的访问修饰符。|`public`|
|多重性|可以扮演相反角色的模型元素数（ `0..1` 、 `1..1` 、 `0..*` 或 `1..*` ）。 如果重数为 `0..*` 或 `1..*` ，则生成的属性表示一个集合; 否则，生成的属性表示一个模型元素。|取决于关系类型以及这是关系中的源角色还是目标角色。|
|“属性”|域角色的名称。 此属性不能包含空格。|此角色的角色扮演者的域类的名称。|
|传播副本|`DoNotPropagateCopy`-复制的角色扮演者将没有此链接的副本。<br /><br /> `PropagateCopyToLinkOnly`-复制的链接指向现有的相反角色扮演者。<br /><br /> `PropagateCopyToLinkAndOppositeRolePlayer`-复制的链接指向相反角色扮演者的副本。|`PropagateCopyToLinkAndOppositeRolePlayer`对于嵌入的源角色。<br /><br /> `DoNotPropagateCopy`对于其他角色。<br /><br /> 有关详细信息，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)|
|传播删除|`True`删除关联链接时，将会扮演此角色的元素。|`True`用于嵌入角色的目标。<br /><br /> `False`对于其他角色。|
|属性名称|在角色扮演者的代码中生成的属性的名称。 此名称不能包含空格。|如果此角色具有零对一或一对一的重数，则相反角色的名称;否则，相反角色的复数名称。|
|角色扮演者|可在关系中扮演此角色的元素的域类。 此属性为只读。|此角色的角色扮演者的域类。|
|备注|与域角色关联的非正式注释。|无 <\>|
|类别|生成的属性在生成的设计器的 "**属性**" 窗口中显示的类别。 如果该属性为空，则生成的属性将显示在 "**杂项**" 类别下|无 <\>|
|描述|用于记录代码并在生成的设计器的 UI 中使用的说明。<br /><br /> 说明显示在角色扮演者类上生成的属性的 IntelliSense 工具提示中。|`Description for`*角色的全名*|
|显示名称|为域角色生成的设计器中显示的名称。|Name 属性的调整后的值。|
|帮助关键字|用于索引域角色的 F1 帮助的可选关键字。|\<none>|
|属性显示名称|为生成的角色属性在生成的设计器中显示的名称。|"属性名称" 属性的调整后的值。|

> [!NOTE]
> 显示名称的默认值基于关联的属性值，方法是在每个大小写字符前面加上一个小写字符，后面不后跟另一个大写字符。

## <a name="see-also"></a>请参阅

- [域关系的属性](../modeling/properties-of-domain-relationships.md)