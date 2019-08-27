---
title: 如何：设置 C/C++ 项目的代码分析属性
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.native
- VC.Project.VCCLCompilerTool.EnablePrefast
- VC.Project.VCFxCopTool.EnablePREfast
- VC.Project.VCFxCopTool.IgnoreGeneratedCode
helpviewer_keywords:
- properties, C/C++ Code Analysis
- properties, Code Analysis
- code analysis properties
- C/C++ code analysis properties
ms.assetid: 7af52097-6d44-4785-9b9f-43b7a7d447d7
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
ms.openlocfilehash: 72866618383382389ad5e5706ae2a0999c89c346
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923989"
---
# <a name="how-to-set-code-analysis-properties-for-cc-projects"></a>如何：设置 C/C++ 项目的代码分析属性
您可以配置代码分析工具用来分析项目的每个配置中的代码的规则。 此外, 您还可以指示代码分析禁止显示由第三方工具生成并添加到项目的代码中的警告。

## <a name="code-analysis-property-page"></a>"代码分析" 属性页
"**代码分析**" 属性页包含项目的所有代码分析配置设置。 若要在**解决方案资源管理器**中打开项目的 "代码分析" 属性页, 请右键单击该项目, 然后单击 "**属性**"。 接下来, 展开 "**配置属性**", 然后选择 "**代码分析**" 选项卡。

## <a name="project-configuration-and-platform"></a>项目配置和平台
使用**配置**列表和**平台**列表, 你可以将不同的代码分析设置应用于不同的项目配置和平台组合。 例如, 你可以指导代码分析将一组规则应用于项目中的调试版本, 并将另一组规则应用于发布版本。

## <a name="enabling-code-analysis"></a>启用代码分析
可以通过选择**C++ "在生成时启用代码分析"** , 来决定是否为项目启用代码分析。 例如, 你可以将与**配置**列表结合使用, 以确定是否对调试版本禁用代码分析并为发布版本启用代码分析。

如果你的项目包含托管代码, 则可以通过选择 **"生成时启用代码分析"** 来决定是启用还是禁用代码分析。

代码分析旨在帮助您改善代码质量并避免常见缺陷。 因此, 请仔细考虑是否禁用代码分析。 通常, 最好禁用规则集或不想应用于项目的单个规则。

## <a name="generated-code"></a>生成的代码
开发人员经常使用工具来帮助快速开发应用程序。 这些工具可生成添加到项目中的代码。 你可能想要查看代码分析在生成的代码中发现的规则冲突。 但是, 如果您不希望维护代码, 则您可能不希望看到它们。

使用 "**常规**属性" 页上的 "**禁止显示生成的代码结果**" 复选框, 您可以选择是否要查看第三方工具生成的托管代码的代码分析警告。

## <a name="rule-sets"></a>规则集
如果你的项目包含托管代码, 则可以通过从 "**运行此规则集**" 列表中选择规则集, 选择要在代码分析中应用的规则。

## <a name="see-also"></a>请参阅

- [分析托管代码质量](../code-quality/code-analysis-for-managed-code-overview.md)
- [C/C++ 代码分析警告](../code-quality/code-analysis-for-c-cpp-warnings.md)