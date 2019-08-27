---
title: 如何：为 ASP.NET Web 应用程序配置代码分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.asp
ms.assetid: b3000b31-fd9d-489e-81a2-a4bee49453ba
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8e75f5a584dd0522240f8b4d45cb28107bca38e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201395"
---
# <a name="how-to-configure-code-analysis-for-an-aspnet-web-application"></a>如何：为 ASP.NET Web 应用程序配置代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在[!INCLUDE[vsPreShort](../includes/vspreshort-md.md)]并[!INCLUDE[vsUltShort](../includes/vsultshort-md.md)]您可以从代码分析的列表中选择*规则集*要应用于[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]Web 应用程序。 默认规则集是 Microsoft Mininimum 建议规则。 您可以选择另一个规则集以将应用于 Web 站点。  
  
### <a name="to-configure-a-rule-set-for-an-aspnet-page-framework-project"></a>为 ASP.NET 页框架项目配置规则集÷  
  
1. 选择中的 Web 站点**解决方案资源管理器**。  
  
2. 上**分析**菜单上，单击**网站上的配置代码分析**。  
  
3. 如果所选解决方案，该解决方案包含多个项目选择的生成配置和目标操作系统从**配置**并**平台**列出。  
  
4. 在解决方案中每个项目，请单击**规则集**列，并单击该规则的名称设置为运行。  
  
5. 默认情况下，对解决方案中的所有项目运行代码分析。 若要禁用或启用特定项目的代码分析，请执行以下步骤：  
  
    1. 右键单击项目名称，然后单击属性。  
  
    2. 选中或清除**时启用代码分析**复选框。 您可以还手动运行代码分析通过选择**网站上运行代码分析**从**分析**菜单。  
  
6. 在中**运行此规则集**下拉列表中，请执行以下步骤：  
  
    - 选择你想要使用的规则集。  
  
    - 选择 **\<浏览 >** 可以指定现有的自定义规则集不在列表中。  
  
    - 定义自定义规则集。 有关详细信息，请参阅[创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)。
