---
title: 代码分析规则集参考
ms.date: 04/04/2018
ms.topic: reference
helpviewer_keywords:
- code analysis, rule sets reference
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fc025a3ff096e560cc2bd5a135f370e89dba2f9e
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91860465"
---
# <a name="code-analysis-rule-set-reference"></a>代码分析规则集参考

在 Visual Studio 中配置托管代码项目的旧分析时，可以从内置 *规则集*列表中进行选择。 某些规则包含在多个内置规则集中，例如，"基本更正规则" 规则集包含 "托管建议规则" 规则集中的规则。

> [!NOTE]
> 本部分中的规则集与旧式分析相关。 有关适用于代码分析器包的规则集的信息，请参阅 [将规则集与代码分析器一起使用](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

您可以使用其中一个内置规则集，也可以 [自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md) 以满足您的项目要求。 如果在自定义规则集中包含多个包含同一规则的规则集，则该规则只在自定义规则集中出现一次。

本节中的主题介绍内置规则集以及它们所包含)  (或警告的规则。

| 规则集 | 包含的规则 |
| - | - |
| [所有规则](all-rules-rule-set.md) | 包含所有可用的托管和 c + + 规则 |
| [基本更正规则](basic-correctness-rules-rule-set-for-managed-code.md) | 包括托管建议规则以及逻辑错误和框架使用情况的规则 |
| [扩展的更正规则](extended-correctness-rules-rule-set-for-managed-code.md) | 包括基本的正确性规则 (，其中包括托管推荐的规则) 以及逻辑错误和框架使用情况的更多规则 |
| [基本设计指南规则](basic-design-guideline-rules-rule-set-for-managed-code.md) | 包括托管建议规则和规则，以确保代码易于阅读、理解和维护 |
| [扩展的设计指南规则](extended-design-guidelines-rules-rule-set-for-managed-code.md) | 包括基本的设计准则规则 (，其中包括托管推荐的规则) 再加上侧重于命名的可维护性规则 |
| [全球化规则](globalization-rules-rule-set-for-managed-code.md) | 包括全球化问题的规则 |
| [托管最低规则](managed-minimum-rules-rule-set-for-managed-code.md) | 对于关键托管代码问题包括四个规则 |
| [托管建议规则](managed-recommended-rules-rule-set-for-managed-code.md) | 包括托管的最小规则以及对关键托管代码问题的更多规则 |
| [混合最低规则](mixed-minimum-rules-rule-set.md) | 包括针对 CLR 的 c + + 代码中的关键问题的规则 |
| [混合建议规则](mixed-recommended-rules-rule-set.md) | 包括混合的最小规则以及用于 CLR c + + 代码中的关键问题的更多规则 |
| [本机最低规则](native-minimum-rules-rule-set.md) | 包括针对本机代码中的关键问题的规则 |
| [本机建议规则](native-recommended-rules-rule-set.md) | 包含本机代码中的严重问题的本机最低规则和更多规则 |
| [安全规则](security-rules-rule-set-for-managed-code.md) | 包括用于查找安全漏洞的规则 |