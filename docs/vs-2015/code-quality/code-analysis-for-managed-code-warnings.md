---
title: 托管代码的代码分析警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vc.project.vcfxcoptool.enablefxcop
helpviewer_keywords:
- managed code analyis, warnings
- warnings, managed code analysis
- managed code analysis warnings
- code analysis,managed code
ms.assetid: 3c2741ff-0d3a-42e6-acd5-d42310bd03c4
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5294840e4669f28f4e8a04978274ad130d1397ee
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535728"
---
# <a name="code-analysis-for-managed-code-warnings"></a>托管代码的代码分析警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

托管代码分析工具可以发出警告，指示托管代码库中存在违反规则的情况。 这些警告将被分类到各个规则领域，例如设计、本地化、性能和安全性。 每个警告表示一次托管代码分析规则冲突。 本部分深入讨论每个托管代码分析警告，并提供相关示例。

 下表显示了为每个警告提供的信息类型。

|Item|说明|
|----------|-----------------|
|类型|规则的 TypeName。|
|CheckId|规则的唯一标识符。 CheckId 和类别用于源代码中禁止显示警告。|
|类别|警告类别。|
|是否重大更改|规则冲突的修复是否是一项重大更改。 重大更改意味着，在导致冲突的目标上具有依赖关系的程序集不会使用新修复的版本重新编译，或者可能会由于此更改在运行时失败。 当具有多个修复可用且至少有一个修复是一项重大更改，有一个不是时，将同时指定“重大”和“非重大”。|
|原因|导致规则生成警告的特定托管代码。|
|描述|讨论警告背后的问题。|
|如何解决冲突|说明如何更改源代码以满足规则并防止它生成警告。|
|何时禁止显示警告|描述何时可以安全地禁止显示此规则警告。|
|示例代码|规则冲突示例和满足该规则的已更正示例。|
|相关警告|相关警告。|

## <a name="in-this-section"></a>本节内容

|项|值|
|-|-|
|[CheckId 的警告](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)|列出按 CheckId 排列的所有警告|
|[加密警告](../code-quality/cryptography-warnings.md)|支持通过正确使用加密机制提高库和应用程序安全的警告。|
|[设计警告](../code-quality/design-warnings.md)|支持由 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 设计准则指定的正确库设计的警告|
|[全球化警告](../code-quality/globalization-warnings.md)|支持世界通用库和应用程序的警告。|
|[互操作性警告](../code-quality/interoperability-warnings.md)|支持与 COM 客户端交互的警告。|
|[可维护性警告](../code-quality/maintainability-warnings.md)|支持库和应用程序维护的警告。|
|[移动性警告](../code-quality/mobility-warnings.md)|支持高效使用电源的警告。|
|[命名警告](../code-quality/naming-warnings.md)|支持遵从 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 设计准则命名约定的警告。|
|[性能警告](../code-quality/performance-warnings.md)|支持高性能库和应用程序的警告。|
|[可移植性警告](../code-quality/portability-warnings.md)|支持跨不同平台的可移植性的警告。|
|[可靠性警告](../code-quality/reliability-warnings.md)|支持库和应用程序可靠性（例如正确使用内存和线程）的警告。|
|[安全警告](../code-quality/security-warnings.md)|支持更安全的库和应用程序的警告。|
|[使用警告](../code-quality/usage-warnings.md)|支持适当使用 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]的警告。|
|[Code Analysis Policy Errors](../code-quality/code-analysis-policy-errors.md)|签入时未满足代码分析策略而发生的错误。|
