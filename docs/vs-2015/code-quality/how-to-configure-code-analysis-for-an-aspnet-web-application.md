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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 423264362118343d573b417cd055d2d722df995e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657464"
---
# <a name="how-to-configure-code-analysis-for-an-aspnet-web-application"></a>如何：为 ASP.NET Web 应用程序配置代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] 和 [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)] 中，可以从要应用到 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序的代码分析*规则集*列表中进行选择。 默认规则集是 Microsoft Mininimum 建议规则。 您可以选择要应用于网站的另一个规则集。

### <a name="to-configure-a-rule-set-for-an-aspnet-page-framework-project"></a>为 ASP.NET 页框架项目配置规则集÷

1. 在**解决方案资源管理器**中选择网站。

2. 在 "**分析**" 菜单上，单击 "**为网站配置代码分析**"。

3. 如果选择了解决方案，但解决方案包含多个项目，请从 "**配置**" 和 "**平台**" 列表中选择 "生成配置" 和 "目标操作系统"。

4. 对于解决方案中的每个项目，单击 "**规则集**" 列，然后单击要运行的规则集的名称。

5. 默认情况下，在解决方案中的所有项目上运行代码分析。 若要禁用或启用特定项目的代码分析，请执行以下步骤：

    1. 右键单击项目名称，然后单击 "属性"。

    2. 选中或清除 "**启用代码分析**" 复选框。 还可以通过在 "**分析**" 菜单中选择 "从网站**运行代码分析**" 来手动运行代码分析。

6. 在 "**运行此规则集**" 下拉列表中，执行以下步骤：

    - 选择要使用的规则集。

    - 选择 **\<Browse >** ，以指定不在列表中的现有自定义规则集。

    - 定义自定义规则集。 有关详细信息，请参阅[创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)。
