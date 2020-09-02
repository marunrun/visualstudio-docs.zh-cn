---
title: 关系图的属性
ms.date: 10/31/2018
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 762c2acb6774d7eb4949087fdd91e85c86acd6bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75595418"
---
# <a name="properties-of-diagrams"></a>关系图的属性
您可以设置属性，以指定关系图在生成的设计器中的显示方式。 例如，可以在关系图中指定文本的默认颜色。

 有关详细信息，请参阅 [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅 [自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 下表列出了关系图的属性。

|属性|说明|默认|
|-|-|-|
|填充颜色|关系图的填充颜色。|白色|
|文本颜色|显示在关系图上的文本的颜色。|黑色|
|访问修饰符|类的访问修饰符 (公共或内部) 。|公用|
|自定义特性|用于将特性添加到生成的代码类。|\<none>|
|生成双派生|如果为 `True` ，则将生成基类和分部类 (来支持通过重写进行自定义) 。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|具有自定义构造函数|如果为 `True` ，则在源代码中提供自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|继承修饰符|描述从关系图 (`none` 、或) 生成的源代码类的继承类型 `abstract` `sealed` 。|无|
|基本关系图|此关系图的基类。|（无）|
|名称|此关系图的名称。|当前名称|
|命名空间|与此关系图关联的命名空间。|当前命名空间|
|表示的类|此关系图表示的根域类。|当前根类（如果适用）|
|备注|与此元素相关联的非正式注释。|\<none>|
|将填充颜色作为属性公开|如果 `True` 为，则用户可以设置生成的设计器的关系图的填充颜色。 若要设置此属性，请右键单击关系图形状，然后单击 "添加" " **公开**"。|错误|
|以属性形式显示文本颜色|如果为 `True` ，则用户可以在生成的设计器中设置关系图的文本颜色。 若要设置此属性，请右键单击关系图形状，然后单击 "添加" " **公开**"。|错误|
|说明|用于记录生成的设计器的说明。|\<none>|
|显示名称|将在此关系图的生成的设计器中显示的名称。|\<none>|
|帮助关键字|用于索引此关系图的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

[域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
