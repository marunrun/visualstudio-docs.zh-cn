---
title: 如何：启用和禁用托管代码的自动代码分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 7c22d194-5fea-4f23-b02d-19344fa64a64
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c4f5de2926cb38f570defa95463489523c694132
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142293"
---
# <a name="how-to-enable-and-disable-automatic-code-analysis-for-managed-code"></a>如何：启用和禁用托管代码的自动代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以配置代码分析，以托管的代码项目中的每次生成之前运行。 可以为每个设置不同的代码分析属性[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]配置。  
  
### <a name="to-enable-or-disable-automatic-code-analysis"></a>若要启用或禁用自动代码分析  
  
1. 在中**解决方案资源管理器**，右键单击该项目，然后单击**属性**。  
  
2. 在项目属性对话框中，单击**代码分析**。  
  
3. 指定在生成类型**配置**和中的目标平台**平台**。  
  
4. 若要启用或禁用自动代码分析，请选择或清除**启用生成代码分析 （定义 CODE_ANALYSIS 常量）** 复选框。
