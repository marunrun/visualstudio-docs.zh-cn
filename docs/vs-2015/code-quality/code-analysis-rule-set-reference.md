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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a1f91b352da5a41ec2ef81fb6067976073c787ef
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62576746"
---
# <a name="code-analysis-rule-set-reference"></a>代码分析规则集参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当配置代码分析托管代码项目中的[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]， [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]，或[!INCLUDE[vsPro](../includes/vspro-md.md)]会显示一系列内置*规则集*。 可以使用某一标准规则集，也可以自定义规则集以适合您的项目要求。  
  
## <a name="available-rule-sets"></a>可用的规则集  
 下表列出了默认规则集：  
  
|||  
|-|-|  
|[“所有规则”规则集](../code-quality/all-rules-rule-set.md)|此规则集包含的所有规则。 运行此规则集可能会导致大量所报告的警告。 使用此规则集可获取代码中的所有问题的概况。 这可以帮助你决定哪一个的更为专注的规则集是最适合运行为你的项目。|  
|[托管代码的“基本更正规则”规则集](../code-quality/basic-correctness-rules-rule-set-for-managed-code.md)|这些规则重点针对逻辑错误和使用的框架 Api 中所犯的常见错误。 包含此规则集以展开报告的最小建议规则警告的列表。|  
|[托管代码的“基本设计准则规则”规则集](../code-quality/basic-design-guideline-rules-rule-set-for-managed-code.md)|这些规则重点针对实施最佳做法，以使代码易于理解和使用。 包含此规则设置，如果你的项目包括库代码，或者如果你想要强制执行的代码更易于维护的最佳实践。|  
|[托管代码的“扩展的更正规则”规则集](../code-quality/extended-correctness-rules-rule-set-for-managed-code.md)|这些规则基于基本正确性规则来最大程度地报告逻辑和框架使用错误扩展。 着重强调了在特定方案如 COM 互操作和移动应用程序上。 请考虑包含此规则集如果其中一种情形适用于你的项目，或在项目中找到其他问题。|  
|[托管代码的“扩展的设计准则规则”规则集](../code-quality/extended-design-guidelines-rules-rule-set-for-managed-code.md)|这些规则基于基本设计准则规则，以最大程度地报告的可用性和可维护性问题进行扩展。 额外的强调置于命名准则。 请考虑包含此规则设置，如果你的项目包括库代码，或者如果你想要强制实施用于编写可维护代码的最高标准。|  
|[托管代码的“全球化规则”规则集](../code-quality/globalization-rules-rule-set-for-managed-code.md)|这些规则重点针对问题而无法正常显示在不同的语言、 区域设置和区域性中使用时在应用程序中的数据。 包含此规则集如果本地化或全球化你的应用程序。|  
|[托管代码的“托管最少量规则”规则集](../code-quality/managed-minimun-rules-rule-set-for-managed-code.md)|这些规则重点在代码中为其代码分析是最准确的最关键问题。  这些规则是数量少，并且它们应仅在有限的 Visual Studio 版本中运行。  与其他 Visual Studio 版本使用 MinimumRecommendedRules.ruleset。|  
|[托管代码的“托管建议规则”规则集](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)|这些规则重点在代码中，包括潜在安全漏洞、 应用程序崩溃和其他重要的逻辑和设计错误的最关键问题。 您应包含任何自定义规则集中设置为你的项目创建此规则。|  
|[“混合最少量规则”规则集](../code-quality/mixed-minimum-rules-rule-set.md)|这些规则重点针对中的最关键问题在C++支持公共语言运行时，包括潜在安全漏洞和应用程序崩溃的项目。 应包含此规则集创建的任何自定义规则集中将C++支持公共语言运行时的项目。|  
|[“混合建议规则”规则集](../code-quality/mixed-recommended-rules-rule-set.md)|这些规则重点关注中最常见和严重问题在C++支持公共语言运行时，包括潜在安全漏洞、 应用程序崩溃和其他重要的逻辑和设计错误的项目。 应包含此规则集创建的任何自定义规则集中将C++支持公共语言运行时的项目。  此规则集旨在与 Visual Studio 专业版和更高版本进行配置。|  
|[“本机最少量规则”规则集](../code-quality/native-minimum-rules-rule-set.md)|这些规则专注于在本机代码中，包括潜在安全漏洞和应用程序崩溃的最关键问题。 应在你为本机项目创建的任何自定义规则集中包含此规则集。|  
|[“本机建议规则”规则集](../code-quality/native-recommended-rules-rule-set.md)|这些规则重点针对本机代码，包括潜在安全漏洞和应用程序崩溃中最重要、 最常见的问题。  应在你为本机项目创建的任何自定义规则集中包含此规则集。  此规则集用于处理与 Visual Studio 专业版和更高版本。|  
|[托管代码的“安全规则”规则集](../code-quality/security-rules-rule-set-for-managed-code.md)|此规则集包含所有 Microsoft 安全性规则。 包含此规则集以最大程度地报告潜在安全问题数。|
