---
title: 如何：设置的 C-代码分析属性C++项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
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
caps.latest.revision: 19
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: 4ebed266924861dac4bfc9e316a56907dbd11534
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201320"
---
# <a name="how-to-set-code-analysis-properties-for-cc-projects"></a>如何：设置 C/C++ 项目的代码分析属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以配置代码分析工具使用来分析每个配置项目中的代码的规则。 此外，还可以指示代码分析禁止显示警告的生成并由第三方工具添加到你的项目的代码。  
  
## <a name="code-analysis-property-page"></a>代码分析属性页  
 **代码分析**属性页包含一个项目的所有代码分析配置设置。 若要打开的项目中的代码分析属性页**解决方案资源管理器**，右键单击项目，然后单击**属性**。 接下来，展开**配置属性**，然后选择**代码分析**选项卡。  
  
## <a name="project-configuration-and-platform"></a>项目配置和平台  
 **配置**列表和**平台**列表，可以将不同的代码分析设置应用于不同的项目配置和平台组合。 例如，可以直接将代码分析，以将一组规则应用到用于调试的项目生成并生成一组不同的版本。  
  
## <a name="enabling-code-analysis"></a>启用代码分析  
 您可以决定是否通过选择启用你的项目的代码分析**启用代码分析的 C /C++上生成**。 结合**配置**列表中，您可以例如，决定禁用调试版本并启用为发布版本的代码分析。  
  
 如果你的项目包含托管的代码，您可以决定是否启用或禁用通过选择代码分析**生成时启用代码分析**。  
  
 代码分析旨在帮助您提高代码质量并避免常见的问题。 因此，请仔细考虑是否要禁用代码分析。 通常，最好禁用规则集或不希望的单个规则应用于你的项目。  
  
## <a name="generated-code"></a>生成的代码  
 开发人员经常使用工具来帮助快速开发应用程序。 这些工具可以生成添加到项目的代码。 您可能想要看到的代码分析在生成的代码中发现的规则冲突。 但是，可能不想要查看它们如果不希望维护代码。  
  
 **禁止显示生成代码的结果**上的复选框**常规**属性页中，可以选择是否想要查看从托管代码中由第三方工具生成的代码分析警告.  
  
## <a name="rule-sets"></a>规则集  
 如果你的项目包含托管的代码，你可以选择要通过选择规则集从应用中的代码分析规则**运行此规则集**列表。  
  
## <a name="see-also"></a>请参阅  
 [分析托管代码质量](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)   
 [C/C++ 代码分析警告](../code-quality/code-analysis-for-c-cpp-warnings.md)
