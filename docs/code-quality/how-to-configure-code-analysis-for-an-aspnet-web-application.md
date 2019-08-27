---
title: 配置 ASP.NET Web 应用程序的代码分析
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.asp
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 51638db2cf258cc1a91c659c137c6a17811fa8c8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62820692"
---
# <a name="how-to-configure-code-analysis-for-an-aspnet-web-application"></a>如何：为 ASP.NET Web 应用程序配置代码分析

在 Visual Studio 中，可以从列表中选择的代码分析*规则集*要应用于[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]web 应用程序。 默认规则集是 Microsoft 最少量建议规则。 您可以选择另一个规则集以将应用于 web 站点。

1. 选择中的 web 站点**解决方案资源管理器**。

2. 上**分析**菜单上，单击**网站上的配置代码分析**。

3. 如果所选解决方案，该解决方案包含多个项目选择的生成配置和目标操作系统从**配置**并**平台**列出。

4. 在解决方案中每个项目，请单击**规则集**列，并单击该规则的名称设置为运行。

5. 默认情况下，对解决方案中的所有项目运行代码分析。 若要禁用或启用特定项目的代码分析，请执行以下步骤：

    1. 右键单击项目名称，然后单击属性。

    2. 选中或清除**时启用代码分析**复选框。 您可以还手动运行代码分析通过选择**网站上运行代码分析**从**分析**菜单。

6. 在中**运行此规则集**下拉列表中，请执行以下步骤：

    - 选择你想要使用的规则集。

    - 选择 **\<浏览 >** 可以指定现有的自定义规则集不在列表中。

    - 定义[自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md)。