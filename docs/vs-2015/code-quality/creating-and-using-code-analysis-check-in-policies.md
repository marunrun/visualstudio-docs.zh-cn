---
title: 创建和使用代码分析签入策略 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: 3fa5a849-e05f-4e31-8ba3-b014c889d94d
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3a8015eb672e87431a1d225221ff2321c41e041a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697051"
---
# <a name="creating-and-using-code-analysis-check-in-policies"></a>创建和使用代码分析签入策略
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你使用 Team Foundation 版本控制 (TFVC) 时，您可以创建代码分析签入策略的.NET Framework 和本机 (C /C++) 代码的团队项目中的项目。 代码分析签入策略可用于控制和改进签入代码库的代码的质量。  
  
 本地生成是最新的和已针对最新源文件运行代码分析时，将传递该策略。 至少，在代码项目中启用代码分析规则必须包含与在团队项目签入策略中定义相同的规则。 已指定为团队项目设置中的错误的规则还必须指定为在代码项目中的错误  
  
> [!IMPORTANT]
> 代码分析签入策略不能应用于网站项目。 它们可以应用于 web 应用程序项目。  
  
 通过使用团队项目设置的创建代码分析签入策略[!INCLUDE[esprscc](../includes/esprscc-md.md)]。 签入策略指定和强制执行团队项目，但代码分析运行是配置和本地开发计算机上运行的单个代码项目。 本部分介绍如何指定代码分析签入策略为团队项目以及如何实现托管代码的自定义代码分析策略。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：创建或更新标准代码分析签入策略](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)  
 介绍用于设置和修改团队项目的代码分析策略的步骤。  
  
 [对托管代码实施自定义签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)  
 介绍使用来创建自定义规则集签入策略的团队项目，并将团队项目的代码项目与签入策略同步的步骤。  
  
 [代码分析签入策略的版本兼容性](../code-quality/version-compatibility-for-code-analysis-check-in-policies.md)  
 介绍了代码分析签入的兼容性问题的不同版本之间[!INCLUDE[vstsLong](../includes/vstslong-md.md)]。  
  
 [如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)  
 介绍如何将单词和标记添加到代码分析命名规则中引用的字典。  
  
## <a name="related-sections"></a>相关章节  
 [设置并强制实施质量要求](https://msdn.microsoft.com/library/bdc5666e-6cf0-45b2-a0a1-133c3f61e852)  
  
 [利用团队项目签入策略提高代码质量](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)
