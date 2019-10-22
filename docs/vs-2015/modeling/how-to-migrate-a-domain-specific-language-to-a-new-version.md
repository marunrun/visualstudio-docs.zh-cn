---
title: 如何：将域特定语言迁移到新版本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6a1ae073-443e-45ca-8bc9-9b944362b449
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 45f7b38f7dbb6ea470b2d9e186dc8e6bf4b33b1e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657331"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>如何：将域特定语言迁移至新版本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以将定义和使用特定于域的语言的项目迁移到使用 [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] 分发的 [!INCLUDE[dsl](../includes/dsl-md.md)] 版本中 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。

 作为 [!INCLUDE[vssdk_current_long](../includes/vssdk-current-long-md.md)] 的一部分提供迁移工具。 此工具可转换使用或定义 DSL 工具 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目和解决方案。

 必须显式运行迁移工具：在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中打开解决方案时，该工具不会自动启动。 可在以下路径找到工具和详细指南文档：

 **% Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>迁移 DSL 项目之前
 迁移工具会修改 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目文件（ **.csproj**）和解决方案文件（ **.sln**）。

#### <a name="to-prepare-projects-for-migration"></a>准备要迁移的项目。

- 请确保可以写入 **.csproj**和 **.sln**文件。 如果它们处于源代码管理下，请确保它们已签出。

- 创建要迁移的文件夹的副本。

## <a name="migrating-a-collection-of-projects"></a>迁移项目集合

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>将 DSL 项目和解决方案迁移到 Visual Studio 2010

1. 启动 DSL 迁移工具。

   - 您可以在 Windows 资源管理器（或文件资源管理器）中双击该工具，或从命令提示符处启动该工具。 该工具位于以下位置：

        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. 选择包含要转换的解决方案和项目的文件夹。

   - 在工具顶部的框中输入路径，或单击 "**浏览**"。

     迁移工具显示定义或使用 Dsl 的项目的树。 该树包括使用**VisualStudio**或**TextTemplating**程序集的每个项目。

3. 查看项目树，并取消选中不希望转换的项目。

   - 选择项目或解决方案以查看该工具将做出的更改列表。

       > [!NOTE]
       > 显示在 "文件夹名称" 旁边的复选框不起作用。 必须展开文件夹才能检查项目和解决方案。

4. 转换项目。

   1. 单击 "**转换**"。

        在转换每个项目文件之前， _project_ **. .csproj**的副本另_存为_**vs2008**

        每个解决方案的**副本均保存为** **vs2008。**

   2. 调查报告的任何失败的转换。

        在文本窗口中报告故障。 此外，树视图还会在未能转换的每个节点上显示一个红色标志。 可以单击节点以获取有关该故障的详细信息。

5. 转换包含成功转换的项目的解决方案中的**所有模板**。

   1. 打开解决方案。

   2. 单击解决方案资源管理器标题中的 "**转换所有模板**" 按钮。

       > [!NOTE]
       > 可以不必要地执行此步骤。 有关详细信息，请参阅[如何自动转换所有模板](https://msdn.microsoft.com/b63cfe20-fe5e-47cc-9506-59b29bca768a)。

6. 更新转换后的项目中的自定义代码。

   - 尝试生成项目，并调查任何故障。

   - 测试设计器。

## <a name="see-also"></a>请参阅
 [可视化和建模 SDK 中的新增功能](../misc/what-s-new-in-visualization-and-modeling-sdk.md)
