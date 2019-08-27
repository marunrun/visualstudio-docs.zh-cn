---
title: 命名警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.namingrules
helpviewer_keywords:
- managed code analysis warnings, naming warnings
- naming warnings
- warnings, naming
ms.assetid: f97223ce-1d39-4134-81c9-fff2c75d979b
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a18e958732094bd445de84d0095b688f2103a67c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552587"
---
# <a name="naming-warnings"></a>命名警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

命名的命名约定的支持遵从性警告[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]设计指导原则。  
  
## <a name="in-this-section"></a>本节内容  
  
|规则|描述|  
|----------|-----------------|  
|[CA1700:未命名的枚举值 Reserved](../code-quality/ca1700-do-not-name-enum-values-reserved.md)|此规则假定当前不使用名称中包含“reserved”的枚举成员，而是将其作为一个占位符，以在将来的版本中重命名或移除它。 重命名或移除成员是一项重大更改。|  
|[CA1713:事件不应具有 before 或 after 前缀](../code-quality/ca1713-events-should-not-have-before-or-after-prefix.md)|事件的名称以“Before”或“After”开头。 若要命名按特定顺序引发的相关事件，请使用现在时或过去时指示一系列操作中的相对位置。|  
|[CA1714:枚举应采用复数形式的名称](../code-quality/ca1714-flags-enums-should-have-plural-names.md)|公共枚举具有 System.FlagsAttribute 特性并且其名称不以"s"结尾。 使用 FlagsAttribute 标记的类型具有采用复数形式，因为该属性指示可以指定多个值的名称。|  
|[CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)|外部可见标识符的名称中包含一个或多个未被 Microsoft 拼写检查器库识别的单词。|  
|[CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)|不能仅通过大小写区分命名空间、类型、成员和参数的标识符，因为针对公共语言运行时的语言不需要区分大小写。|  
|[CA1715:标识符应具有正确的前缀](../code-quality/ca1715-identifiers-should-have-correct-prefix.md)|外部可见的接口的名称不以大写的"I"开头。  上的外部可见类型或方法的泛型类型参数的名称不以大写"T"开头。|  
|[CA1720:标识符不应包含类型名称](../code-quality/ca1720-identifiers-should-not-contain-type-names.md)|外部可见成员中的某个参数的名称包含一个数据类型名称，或者外部可见成员的名称包含一个语言特定的数据类型名称。|  
|[CA1722:标识符应采用正确的前缀](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)|按照约定，只有某些编程元素具有以特定前缀开头的名称。|  
|[CA1711:标识符应采用正确的后缀](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)|按照约定，只有扩展某些基类型或实现某些接口的类型的名称或者从这些类型派生的类型的名称，应该以特定的保留后缀结尾。 其他类型名称不应使用这些保留的后缀。|  
|[CA1717:只有 FlagsAttribute 枚举应采用复数形式的名称](../code-quality/ca1717-only-flagsattribute-enums-should-have-plural-names.md)|命名约定规定，复数形式的枚举名称表示可以同时指定多个枚举值。|  
|[CA1725:参数名应与基声明](../code-quality/ca1725-parameter-names-should-match-base-declaration.md)|以一致的方式命名重写层次结构中的参数可以提高方法重写的可用性。 如果派生方法中的参数名与基声明中的名称不同，可能会导致无法区分出该方法是基方法的重写还是该方法的新重载。|  
|[CA1719:参数名不应与成员名称](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)|参数名称应传达参数的含义和成员名称应传达成员的含义。 两者相同的设计非常少见。 使参数与其成员同名会导致不直观的效果，会使库难以使用。|  
|[CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)|每个单词中的资源字符串拆分为根据大小写的令牌。 Microsoft 拼写检查器库会对由两个连续的标记构成的每个组合进行检查。 如果被识别，该单词将生成规则冲突。|  
|[CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)|资源字符串包含一个或多个未被 Microsoft 拼写检查器库识别的单词。|  
|[CA1724:类型名不应与命名空间](../code-quality/ca1724-type-names-should-not-match-namespaces.md)|类型名称不应该与 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类库中定义的命名空间的名称匹配。 此规则的冲突会降低库的可用性。|  
|[CA1707:标识符不应包含下划线](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)|按照约定，标识符名称不包含下划线 (_) 字符。 该规则将检查命名空间、类型、成员和参数。|  
|[CA1721:属性名不应与 get 方法](../code-quality/ca1721-property-names-should-not-match-get-methods.md)|公共或受保护成员的名称以“Get”开头，且其余部分与公共或受保护属性的名称匹配。 “Get”方法和属性的名称应能够明确区分其功能上的差异。|  
|[CA1716:标识符不应与关键字](../code-quality/ca1716-identifiers-should-not-match-keywords.md)|某个命名空间名称或类型名称与编程语言中的保留关键字相同。 命名空间和类型的标识符不应与针对公共语言运行时的语言所定义的关键字冲突。|  
|[CA1726:使用首选的词条](../code-quality/ca1726-use-preferred-terms.md)|在外部可见的标识符的名称中，包括一个存在首选备用词条的词条。 或者，名称中包含“Flag”或“Flags”一词。|  
|[CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)|按照约定，参数名称使用驼峰式大小写和命名空间中，类型和成员名称使用 Pascal 大小写。|  
|[CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)|标识符的名称包含多个单词，其中至少有一个单词似乎是大小写不正确的组合词。|  
|[CA1712:不要使用类型名称的枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)|由于类型信息需要由开发工具提供的枚举成员的名称将不使用前缀的类型名称。|  
|[CA1710:标识符应具有正确的后缀](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)|按照约定，类型扩展某些基类型或实现特定接口或从这些类型派生的类型的名称具有与基类型或接口关联的后缀。|
