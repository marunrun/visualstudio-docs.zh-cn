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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8e31ff799edc93d250eeeab57b349873a63ecf14
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667715"
---
# <a name="creating-and-using-code-analysis-check-in-policies"></a>创建和使用代码分析签入策略
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 Team Foundation 版本控制（TFVC）时，可以为团队项目中的 .NET Framework 和本机（C/C++）代码项目创建代码分析签入策略。 您可以使用代码分析签入策略来控制和提高签入到代码库中的代码的质量。

 当本地生成是最新的，并且代码分析已在最新的源文件上运行时，策略将通过。 在代码项目中启用的代码分析规则至少必须包含与团队项目签入策略中定义的规则相同的规则。 在团队项目设置中已指定为错误的规则还必须在代码项目中指定为错误

> [!IMPORTANT]
> 代码分析签入策略不能应用于网站项目。 它们可以应用于 web 应用程序项目。

 您可以使用的团队项目设置来创建代码分析签入策略 [!INCLUDE[esprscc](../includes/esprscc-md.md)]。 为团队项目指定并强制执行签入策略，但为本地开发计算机上的单个代码项目配置和运行代码分析。 本节介绍如何为团队项目指定代码分析签入策略，以及如何为托管代码实现自定义代码分析策略。

## <a name="in-this-section"></a>本节内容
 [如何：创建或更新标准代码分析签入策略](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)说明用于为团队项目设置和修改代码分析策略的步骤。

 [为托管代码实现自定义签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)说明用于为团队项目的签入策略创建自定义规则集的步骤，以及用于将团队项目的代码项目与签入策略进行同步的步骤。

 [代码分析签入策略的版本兼容性](../code-quality/version-compatibility-for-code-analysis-check-in-policies.md)说明 [!INCLUDE[vstsLong](../includes/vstslong-md.md)] 版本之间的代码分析签入兼容性问题。

 [如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)说明如何向代码分析命名规则中引用的字典添加单词和标记。

## <a name="related-sections"></a>相关章节
 [设置并强制实施质量要求](https://msdn.microsoft.com/library/bdc5666e-6cf0-45b2-a0a1-133c3f61e852)

 [利用团队项目签入策略提高代码质量](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)
