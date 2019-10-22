---
title: 代码分析规则集引用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- code analysis, rule sets
ms.assetid: 5874e854-e298-4d2e-bbe4-95e899d22587
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a3c0b347f186c5adee6cf86a0e1720ebfa80f253
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670117"
---
# <a name="code-analysis-rule-set-reference"></a>代码分析规则集参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 中配置托管代码项目的代码分析时，[!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] 或 [!INCLUDE[vsPro](../includes/vspro-md.md)]you 将显示内置*规则集*的列表。 可以使用某一标准规则集，也可以自定义规则集以适合您的项目要求。

## <a name="available-rule-sets"></a>可用规则集
 下表列出了默认规则集：

|||
|-|-|
|[“所有规则”规则集](../code-quality/all-rules-rule-set.md)|此规则集包含所有规则。 运行此规则集可能会导致报告大量警告。 使用此规则集可全面了解代码中的所有问题。 这可以帮助你确定哪些更为集中的规则集最适用于你的项目。|
|[托管代码的“基本更正规则”规则集](../code-quality/basic-correctness-rules-rule-set-for-managed-code.md)|这些规则重点介绍了在使用框架 Api 时的逻辑错误和常见错误。 包含此规则集以便在建议的最低规则报告的警告列表中进行扩展。|
|[托管代码的“基本设计准则规则”规则集](../code-quality/basic-design-guideline-rules-rule-set-for-managed-code.md)|这些规则侧重于强制实施最佳实践，使代码易于理解和使用。 如果你的项目包含库代码，或者如果你要强制实施最佳实践来轻松维护代码，请包含此规则集。|
|[托管代码的“扩展的更正规则”规则集](../code-quality/extended-correctness-rules-rule-set-for-managed-code.md)|这些规则对基本更正规则进行了扩展，以最大程度地提高所报告的逻辑和框架使用错误。 对特定方案（如 COM 互操作和移动应用程序）施加了额外的强调。 如果其中一个方案适用于你的项目或在项目中发现其他问题，请考虑包含此规则集。|
|[托管代码的“扩展的设计准则规则”规则集](../code-quality/extended-design-guidelines-rules-rule-set-for-managed-code.md)|这些规则对基本设计准则规则进行了扩展，以最大程度地提高所报告的可用性和可维护性问题。 特别强调的是命名准则。 如果你的项目包含库代码，或者如果你想要强制编写可维护代码的最高标准，请考虑包含此规则集。|
|[托管代码的“全球化规则”规则集](../code-quality/globalization-rules-rule-set-for-managed-code.md)|这些规则重点介绍在不同语言、区域设置和区域性中使用时阻止应用程序中的数据正确显示的问题。 如果你的应用程序已本地化或全球化，请包含此规则集。|
|[托管代码的“托管最少量规则”规则集](../code-quality/managed-minimun-rules-rule-set-for-managed-code.md)|这些规则侧重于代码中最关键的问题，代码分析最准确。  这些规则的数量较少，只适用于在有限的 Visual Studio 版本中运行。  将 MinimumRecommendedRules 与其他 Visual Studio 版本结合使用。|
|[托管代码的“托管建议规则”规则集](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)|这些规则侧重于代码中最关键的问题，包括潜在的安全漏洞、应用程序崩溃和其他重要的逻辑和设计错误。 应在为项目创建的任何自定义规则集中包含此规则集。|
|[“混合最少量规则”规则集](../code-quality/mixed-minimum-rules-rule-set.md)|这些规则重点介绍支持公共语言运行时的C++项目中最关键的问题，包括潜在的安全漏洞和应用程序崩溃。 应在为支持公共语言运行时的C++项目创建的任何自定义规则集中包含此规则集。|
|[“混合建议规则”规则集](../code-quality/mixed-recommended-rules-rule-set.md)|这些规则重点介绍支持公共语言运行时的C++项目中最常见和最关键的问题，包括潜在的安全漏洞、应用程序崩溃和其他重要的逻辑和设计错误。 应在为支持公共语言运行时的C++项目创建的任何自定义规则集中包含此规则集。  此规则集设计用于配置 Visual Studio Professional 版本和更高版本。|
|[“本机最少量规则”规则集](../code-quality/native-minimum-rules-rule-set.md)|这些规则重点关注本机代码中的最关键问题，包括潜在的安全漏洞和应用程序崩溃。 应在你为本机项目创建的任何自定义规则集中包含此规则集。|
|[“本机建议规则”规则集](../code-quality/native-recommended-rules-rule-set.md)|这些规则重点关注本机代码中最关键的问题，包括潜在的安全漏洞和应用程序崩溃。  应在你为本机项目创建的任何自定义规则集中包含此规则集。  此规则集旨在与 Visual Studio Professional 版和更高版本结合使用。|
|[托管代码的“安全规则”规则集](../code-quality/security-rules-rule-set-for-managed-code.md)|此规则集包含所有 Microsoft 安全规则。 包含此规则集可最大程度地提高所报告的潜在安全问题的数量。|
