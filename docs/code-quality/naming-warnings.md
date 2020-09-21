---
title: 命名规则
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.namingrules
helpviewer_keywords:
- managed code analysis rules, naming rules
- naming rules
- rules, naming
ms.assetid: f97223ce-1d39-4134-81c9-fff2c75d979b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2032a66837ef790ce37ef178805a13841f203342
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810189"
---
# <a name="naming-rules"></a>命名规则

命名规则支持遵从 .NET 设计准则的命名约定。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA1700:不要命名“Reserved”枚举值](../code-quality/ca1700.md)|此规则假定当前不使用名称中包含“reserved”的枚举成员，而是将其作为一个占位符，以在将来的版本中重命名或移除它。 重命名或移除成员是一项重大更改。|
|[CA1707:标识符不应包含下划线](../code-quality/ca1707.md)|按照约定，标识符名称不包含下划线 (_) 字符。 该规则将检查命名空间、类型、成员和参数。|
|[CA1708:标识符应以大小写之外的差别进行区分](../code-quality/ca1708.md)|不能仅通过大小写区分命名空间、类型、成员和参数的标识符，因为针对公共语言运行时的语言不需要区分大小写。|
|[CA1710:标识符应具有正确的后缀](../code-quality/ca1710.md)|按照约定，扩展某些基类型或实现某些接口的类型的名称或从这些类型派生的类型具有与基类型或接口关联的后缀。|
|[CA1711:标识符应采用正确的后缀](../code-quality/ca1711.md)|按照约定，只有扩展某些基类型或实现某些接口的类型的名称或者从这些类型派生的类型的名称，应该以特定的保留后缀结尾。 其他类型名称不应使用这些保留的后缀。|
|[CA1712:不要将类型名用作枚举值的前缀](../code-quality/ca1712.md)|枚举成员的名称不带有类型名称前缀，因为开发工具应提供类型信息。|
|[CA1713:事件不应具有 before 或 after 前缀](../code-quality/ca1713.md)|事件的名称以“Before”或“After”开头。 若要命名按特定顺序引发的相关事件，请使用现在时或过去时指示一系列操作中的相对位置。|
|[CA1714:Flags 枚举应采用复数形式的名称](../code-quality/ca1714.md)|公共枚举具有 FlagsAttribute 属性，其名称不以 "s" 结尾。 用 FlagsAttribute 标记的类型的名称是复数，因为该属性指示可以指定多个值。|
|[CA1715:标识符应具有正确的前缀](../code-quality/ca1715.md)|外部可见接口的名称不以大写的 "I" 开头。  外部可见类型或方法的泛型类型参数的名称不以大写 "T" 开头。|
|[CA1716:标识符不应与关键字冲突](../code-quality/ca1716.md)|某个命名空间名称或类型名称与编程语言中的保留关键字相同。 命名空间和类型的标识符不应与针对公共语言运行时的语言所定义的关键字冲突。|
|[CA1717:只有 FlagsAttribute 枚举应采用复数形式的名称](../code-quality/ca1717.md)|命名约定规定，复数形式的枚举名称表示可以同时指定多个枚举值。|
|[CA1720:标识符不应包含类型名称](../code-quality/ca1720.md)|外部可见成员中的某个参数的名称包含一个数据类型名称，或者外部可见成员的名称包含一个语言特定的数据类型名称。|
|[CA1721:属性名不应与 get 方法冲突](../code-quality/ca1721.md)|公共或受保护成员的名称以“Get”开头，且其余部分与公共或受保护属性的名称匹配。 “Get”方法和属性的名称应能够明确区分其功能上的差异。|
|[CA1724:类型名不应与命名空间冲突](../code-quality/ca1724.md)|类型名不应与 .NET 命名空间的名称相匹配。 违反此规则会降低库的可用性。|
|[CA1725:参数名应与基方法中的声明保持一致](../code-quality/ca1725.md)|以一致的方式命名重写层次结构中的参数可以提高方法重写的可用性。 如果派生方法中的参数名与基声明中的名称不同，可能会导致无法区分出该方法是基方法的重写还是该方法的新重载。|
