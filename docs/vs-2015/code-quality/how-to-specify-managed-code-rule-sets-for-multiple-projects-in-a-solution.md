---
title: 如何：为解决方案中的多个项目指定托管代码规则集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.solution
ms.assetid: 92dc3250-a010-4396-b515-f03a0b30cd2a
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e5333f6133dd3fd56077c14d6e56cd6fdada4404
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656427"
---
# <a name="how-to-specify-managed-code-rule-sets-for-multiple-projects-in-a-solution"></a>如何：为解决方案中的多个项目指定托管代码规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，将为解决方案的所有托管项目分配 "Microsoft 最低建议规则" 代码分析*规则集*。 可以在解决方案的 "属性" 对话框中更改分配给解决方案项目的规则集。

> [!NOTE]
> 默认情况下，不会将项目代码分析作为生成步骤运行。 若要启用代码分析作为生成步骤，请参阅[如何：配置托管代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)。

### <a name="to-specify-a-rule-set-for-multiple-projects-in-a-managed-code--solution"></a>为托管代码解决方案中的多个项目指定规则集

1. 在 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]。 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] 或 [!INCLUDE[vsPro](../includes/vspro-md.md)]中，打开解决方案。

2. 在 "**分析**" 菜单上，单击 "**为解决方案配置代码分析**"。

3. 如有必要，展开 "**通用属性**"，然后单击 "**代码分析设置**"。

4. 你可以为一个或多个项目指定规则集。

    - 若要为单个项目指定规则集，请单击项目名称。

    - 若要为多个项目指定规则集，请按住 CTRL 并单击项目名称。

    - 若要指定解决方案中的所有项目，请按住 SHIFT，并单击项目列表。

5. 单击项目的 "**规则集**" 字段，然后单击要应用的规则集的名称。
