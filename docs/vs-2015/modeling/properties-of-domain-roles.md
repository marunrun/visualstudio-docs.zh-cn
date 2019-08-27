---
title: 域角色的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
ms.assetid: 5a7bb18c-638e-45e8-9d79-9aa6a9e14b0e
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b78c409a761a98439cbbbfdf088e052eca745f32
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444464"
---
# <a name="properties-of-domain-roles"></a>域角色的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

下表中的属性是与域角色相关联。 域角色的信息，请参阅[了解模型、 类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。  
  
|属性|描述|默认|  
|--------------|-----------------|-------------|  
|集合类型|如果此角色的重数为 0..* 或 1...\*，此属性自定义的泛型类型的用于存储的链接的集合。|`(none)` - <xref:Microsoft.VisualStudio.Modeling.LinkedElementCollection%601> 使用|  
|自定义特性|你在此处指定的属性将作为属性添加到生成的代码类。|\<none>|  
|属性是可浏览|如果`True`，如果关系的多重性 0..1 或 1..1，可以在用户浏览角色属性和**属性**窗口。 属性显示在另一端的关系链接元素的名称。|`True`|  
|是属性生成器|如果`True`，对于此角色，可用于遍历在程序代码中的关系生成角色属性。 如果将其设置 false，则可以通过使用域关系的静态方法效率较低的方式遍历关系。|`True`|  
|属性 Getter 访问修饰符|生成的属性的 getter 访问修饰符 (`public`， `internal`， `private`， `protected`，或`protected internal`)。|`public`|  
|属性 Setter 访问修饰符|生成的属性的 setter 访问修饰符 (`public`， `internal`， `private`， `protected`，或`protected internal`)。|`public`|  
|重数|这可以播放的对方角色的模型元素的数量 (`0..1`， `1..1`， `0..*`，或`1..*`)。 如果重数`0..*`或`1..*`，则生成的属性表示的集合; 否则，生成的属性表示单个模型元素。|依赖关系类型以及是否这是关系中的源或目标角色。|  
|名称|域角色的名称。 此属性不能包含空格。|此角色的角色扮演者的域类的名称。|  
|将复制传播|`DoNotPropagateCopy` -复制的角色扮演者将拥有此链接的任何副本。<br /><br /> `PropagateCopyToLinkOnly` -复制的链接将指向现有相反角色扮演者。<br /><br /> `PropagateCopyToLinkAndOppositeRolePlayer` -将复制的链接指向一份相反角色扮演者。|`PropagateCopyToLinkAndOppositeRolePlayer` 嵌入的源角色。<br /><br /> `DoNotPropagateCopy` 对于其他角色。<br /><br /> 有关详细信息，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)|  
|将删除传播|`True` 若要删除的关联的链接，删除时播放此角色的元素。|`True` 有关嵌入角色的目标。<br /><br /> `False` 对于其他角色。<br /><br /> 有关详细信息，请参阅[自定义删除行为](../modeling/customizing-deletion-behavior.md)。|  
|属性名|角色扮演者的代码中生成的属性的名称。 此名称不能包含空格。|如果此角色具有零对一的对方角色的名称或一对一的重数;否则为对方角色的复数的名称。|  
|角色扮演者|可以在关系中扮演此角色的元素的域类。 此属性是只读的。|此角色的角色扮演者的域类。|  
|说明|域角色相关联的非正式说明。|\<none>|  
|类别|在其下生成的属性显示在类别**属性**中生成的设计器窗口。 如果此属性为空，则生成的属性下会出现**杂项**类别|\<none>|  
|描述|说明用于记录代码和生成的设计器在 UI 中使用。<br /><br /> 角色扮演者类上生成的属性的 Intellisense 工具提示中显示的描述。|`Description for` *角色的完整名称*|  
|显示名称|域角色生成的设计器中显示的名称。|Name 属性的调整后的值。|  
|帮助关键字|可选的关键字用于编制索引的域角色的 F1 帮助。|\<none>|  
|属性显示名称|在生成的设计器生成的角色属性中显示的名称。|调整后的值的属性名称属性。|  
  
> [!NOTE]
> 显示名称的默认值基于关联的属性值插入每个大写字符小写字符前面和未跟一个大写字符之前的空格。  
  
## <a name="see-also"></a>请参阅  
 [域关系的属性](../modeling/properties-of-domain-relationships.md)
