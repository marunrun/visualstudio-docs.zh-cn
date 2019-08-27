---
title: 如何：配置托管的代码项目的代码分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.csvb
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
ms.assetid: 618f6ff3-db0e-46cb-b08d-dfa35e62c9e7
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a37ededab38cf27a002117f874d17d6a340000d9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63429169"
---
# <a name="how-to-configure-code-analysis-for-a-managed-code-project"></a>如何：为托管代码项目配置代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在[!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]，[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]并[!INCLUDE[vsPro](../includes/vspro-md.md)]，可以选择从一组代码分析*规则集*要应用于托管的代码项目。 默认规则集是 Microsoft 最少量建议规则。 您可以应用其他规则设置为一个项目或解决方案中的所有项目。  
  
> [!NOTE]
> 有关如何配置 ASP.NET Web 应用程序设置的规则的信息，请参阅[如何：为 ASP.NET Web 应用程序配置代码分析](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)。  
  
### <a name="to-configure-a-rule-set-for-a-net-framework-project"></a>若要配置的规则设置为.NET Framework 项目  
  
1. 在中**解决方案资源管理器**，单击该项目。  
  
2. 上**分析**菜单上，单击**的配置代码分析** *ProjectName*。  
  
3. 在中**配置**并**平台**列表中，单击生成配置和目标平台。  
  
4. 若要运行代码分析，每次使用所选的配置生成项目，选择**启用生成代码分析 （定义 CODE_ANALYSIS 常量）** 复选框。 您可以还手动运行代码分析通过打开**分析**菜单，然后单击**上运行代码分析** *ProjectName*。  
  
5. 默认情况下，代码分析不报告由外部工具自动生成的代码所产生的警告。 若要查看生成的代码，请清除**禁止显示生成代码的结果**复选框。  
  
    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码。  
  
6. 在中**运行此规则集**列表中，执行下列操作之一：  
  
    - 单击你想要使用的规则集。  
  
    - 单击 **\<浏览...>** 可以指定现有的自定义规则集不在列表中。  
  
    - 定义自定义规则集。  
  
         有关详细信息，请参阅[创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)。  
  
## <a name="see-also"></a>请参阅  
 [演练：配置和使用自定义规则设置](../code-quality/walkthrough-configuring-and-using-a-custom-rule-set.md)
