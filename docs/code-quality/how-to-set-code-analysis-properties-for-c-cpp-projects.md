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
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 27f3d68d28b8d1799c52fcf83c6a00dc5f81f48a
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72448916"
---
# <a name="how-to-set-code-analysis-properties-for-cc-projects"></a>如何：设置 C/C++ 项目的代码分析属性

您可以配置代码分析工具用来分析项目的每个配置中的代码的规则。 此外，您还可以指示代码分析禁止显示由第三方工具生成并添加到项目的代码中的警告。

## <a name="code-analysis-property-page"></a>"代码分析" 属性页

"**代码分析**" 属性页包含 MSBuild 项目的所有代码分析配置设置。 若要在**解决方案资源管理器**中打开项目的 "代码分析" 属性页，请右键单击该项目，然后单击 "**属性**"。 接下来，展开 "**配置属性**"，然后选择 "**代码分析**" 选项卡。

## <a name="project-configuration-and-platform"></a>项目配置和平台

使用窗口顶部的 "**配置**列表和**平台**" 列表，您可以将不同的代码分析设置应用于不同的项目配置和平台组合。 例如，你可以指导代码分析将一组规则应用于项目中的调试版本，并将另一组规则应用于发布版本。

## <a name="enabling-code-analysis"></a>启用代码分析

通过选择 "**生成时启用代码分析**"，可以通过切换 "**启用 Microsoft 代码分析**" 并**启用 Clang**选项，进一步配置是否在生成时运行项目的代码分析。 例如，你可以将与**配置**列表结合使用，以确定是否对调试版本禁用代码分析并为发布版本启用代码分析。

代码分析旨在帮助您改善代码质量并避免常见缺陷。 因此，请仔细考虑是否禁用代码分析。 通常可以更好地禁用规则集、单个规则或不想应用于项目的单个检查。

## <a name="cmake-configuration"></a>CMake 配置

在 CMake 项目中，更改 "`enableMicrosoftCodeAnalysis`" 和 "`enableClangTidyCodeAnalysis` `CMakeSettings.json` 中" 键的值，以启用或禁用代码分析。 有关详细信息，请参阅[在 Visual Studio 中使用 Clang-整洁](../code-quality/clang-tidy.md)。

## <a name="see-also"></a>请参阅

- [分析托管代码质量](../code-quality/code-analysis-for-managed-code-overview.md)
- [C/C++ 代码分析警告](../code-quality/code-analysis-for-c-cpp-warnings.md)
- [代码的C++规则集](../code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run.md)
- [使用 Clang](../code-quality/clang-tidy.md)
