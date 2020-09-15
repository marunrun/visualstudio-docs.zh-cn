---
title: 托管代码的代码分析警告
ms.date: 08/31/2020
ms.topic: reference
f1_keywords:
- vc.project.vcfxcoptool.enablefxcop
helpviewer_keywords:
- managed code analyis, warnings
- warnings, managed code analysis
- managed code analysis warnings
- code analysis,managed code
ms.assetid: 3c2741ff-0d3a-42e6-acd5-d42310bd03c4
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 566b9827f42f646cd9350cfc015a460485212a09
ms.sourcegitcommit: a18c7e9b367c2f92f6e54c3eaef442775d457667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90094325"
---
# <a name="net-code-analysis-rules"></a>.NET 代码分析规则
.NET 代码分析提供的规则指出了代码质量冲突或建议以提高代码质量。 这些规则组织为规则领域，例如设计、本地化、性能和安全性。 某些规则特定于 .NET API 的使用情况，而其余规则则与一般代码质量有关。 本部分提供了有关每个规则的详细讨论和示例。

 下表显示了为每个诊断提供的信息类型。

|Item|说明|
|----------|-----------------|
|类型|规则的 TypeName。|
|RuleId|规则的唯一标识符。 RuleId 和 Category 用于在源代码中禁止显示警告。|
|类别|警告类别。|
|重大更改|规则冲突的修复是否是一项重大更改。 重大更改意味着，在导致冲突的目标上具有依赖关系的程序集不会使用新修复的版本重新编译，或者可能会由于此更改在运行时失败。 如果有多个修补程序，并且至少有一个修复是重大更改，且一个修补程序不是，则同时指定了 "中断" 和 "非换行"。|
|原因|导致规则生成警告的特定托管代码。|
|说明|讨论警告背后的问题。|
|如何解决冲突|说明如何更改源代码以满足规则并防止它生成警告。|
|何时禁止显示警告|描述何时可以安全地禁止显示此规则警告。|
|示例代码|规则冲突示例和满足该规则的已更正示例。|
|相关警告|相关警告。|

## <a name="in-this-section"></a>本节内容

|类别|说明|
|-|-|
|[按 ID 的规则](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)|按 RuleID 列出所有规则|
|[设计规则](../code-quality/design-warnings.md)|支持由 .NET 设计准则指定的正确库设计的规则。|
|[文档规则](../code-quality/documentation-warnings.md)|通过正确使用 XML 文档注释，支持记录良好的库设计的规则。|
|[全球化规则](../code-quality/globalization-warnings.md)|支持世界通用库和应用程序的规则。|
|[可维护性规则](../code-quality/maintainability-warnings.md)|支持库和应用程序维护的规则。|
|[命名规则](../code-quality/naming-warnings.md)|支持遵守 .NET 设计准则命名约定的规则。|
|[性能规则](../code-quality/performance-warnings.md)|支持高性能库和应用程序的规则。|
|[可移植性和互操作性规则](../code-quality/interoperability-warnings.md)|支持跨不同平台的可移植性和与 COM 客户端交互的规则。|
|[发布规则](../code-quality/publish-warnings.md)|支持适当发布 .NET 应用程序的规则。|
|[可靠性规则](../code-quality/reliability-warnings.md)|支持库和应用程序可靠性（例如正确的内存和线程使用）的规则。|
|[安全性规则](../code-quality/security-warnings.md)|支持更安全的库和应用程序的规则。|
|[使用规则](../code-quality/usage-warnings.md)|支持 .NET 的适当用法的规则。|
