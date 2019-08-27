---
title: 如何：个解决方案中的多个项目指定托管的代码规则集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.solution
ms.assetid: 92dc3250-a010-4396-b515-f03a0b30cd2a
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 555f8cb0ace4386a3fba7730980295dc16e58b2a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63426673"
---
# <a name="how-to-specify-managed-code-rule-sets-for-multiple-projects-in-a-solution"></a>如何：为解决方案中的多个项目指定托管的代码规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，解决方案的所有托管的项目会获得 Microsoft 最少量建议规则代码分析*规则集*。 您可以更改分配给该解决方案的属性对话框中的解决方案的项目的规则集。  
  
> [!NOTE]
> 默认情况下，不是作为生成步骤运行项目代码分析。 若要启用代码分析作为生成步骤，请参阅[如何：配置托管的代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)。  
  
### <a name="to-specify-a-rule-set-for-multiple-projects-in-a-managed-code--solution"></a>若要指定一个规则设置对于托管的代码解决方案中的多个项目  
  
1. 在[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]。 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] 或 [!INCLUDE[vsPro](../includes/vspro-md.md)]中，打开解决方案。  
  
2. 上**分析**菜单上，单击**为解决方案配置代码分析**。  
  
3. 如有必要，展开**常见属性**，然后单击**代码分析设置**。  
  
4. 可以指定的一个或多个项目设置的规则。  
  
    - 若要指定规则集为单个项目，单击项目名称。  
  
    - 若要指定多个项目设置的规则，请按住 ctrl 键并单击项目名称。  
  
    - 若要在解决方案中指定的所有项目，按住 SHIFT 并单击项目列表中。  
  
5. 单击**规则集**字段的项目，然后单击你想要应用规则的名称设置。
