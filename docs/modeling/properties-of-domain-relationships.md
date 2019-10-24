---
title: 域关系的属性
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d08f453c3c52f8520dacc26f9b636fd8c8bcafde
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747476"
---
# <a name="properties-of-domain-relationships"></a>域关系的属性
下表中的属性与域关系关联。 有关域关系的信息，请参阅[了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|Property|描述|Default|
|-|-|-|
|访问修饰符|域关系（`public` 或 `internal`）的访问级别。|`public`|
|自定义特性|用于向从域关系生成的源代码类添加特性。|\<none>|
|生成双派生|如果 `True`，则生成基类和分部类（以支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|具有自定义构造函数|如果 `True`，则指示在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|继承修饰符|描述从域关系（`none`、`abstract` 或 `sealed`）生成的源代码类的继承类型。|\<none>|
|允许重复项|如果 `True`，则可以在相同的两个元素之间创建域关系的重复链接。|`False`|
|基本关系|如果域关系是派生的，则为域关系的基本关系。|\<none>|
|为嵌入|如果 `True`，则域关系是嵌入关系。 如果 `False`，则关系是引用关系。|\<both >|
|“属性”|域关系的名称。|当前名称|
|Namespace|与域关系关联的命名空间。|当前命名空间|
|注意|与域关系关联的非正式注释。|\<none>|
|描述|用于记录代码并在生成的设计器的 UI 中使用的说明。|\<none>|
|显示名称|为域关系生成的设计器中显示的名称。|\<none>|
|帮助关键字|用于索引域关系的 F1 帮助的可选关键字。|\<none>|

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)