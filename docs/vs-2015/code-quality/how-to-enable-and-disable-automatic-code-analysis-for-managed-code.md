---
title: 如何：为托管代码启用和禁用自动代码分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 7c22d194-5fea-4f23-b02d-19344fa64a64
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d87cc57b31e63ae7aafa53c335df2b56f86a0409
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658102"
---
# <a name="how-to-enable-and-disable-automatic-code-analysis-for-managed-code"></a>如何：启用和禁用托管代码的自动代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以将代码分析配置为在托管代码项目的每个内部版本之前运行。 可以为每个 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 配置设置不同的代码分析属性。

### <a name="to-enable-or-disable-automatic-code-analysis"></a>启用或禁用自动代码分析

1. 在**解决方案资源管理器**中，右键单击该项目，然后单击 "**属性**"。

2. 在项目的 "属性" 对话框中，单击 "**代码分析**"。

3. 在**配置**中指定生成类型，并在**平台**中指定目标平台。

4. 若要启用或禁用自动代码分析，请选中或清除 "**生成时启用代码分析（定义 CODE_ANALYSIS 常量）** " 复选框。
