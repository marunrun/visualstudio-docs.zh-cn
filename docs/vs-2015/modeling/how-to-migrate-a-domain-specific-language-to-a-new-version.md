---
title: 如何：将域特定语言迁移至新版本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6a1ae073-443e-45ca-8bc9-9b944362b449
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7f3cefc7c6e2a78d757bb931a430f09c6da103c1
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681048"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>如何：将域特定语言迁移至新版本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以迁移项目的定义和使用特定于域的语言设置为[!INCLUDE[vs2010](../includes/vs2010-md.md)]的版本从[!INCLUDE[dsl](../includes/dsl-md.md)]一起分发[!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)]。  
  
 作为的一部分提供迁移工具[!INCLUDE[vssdk_current_long](../includes/vssdk-current-long-md.md)]。 该工具将为[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]项目和解决方案的使用或定义 DSL 工具。  
  
 您必须显式运行迁移工具： 它就不会启动自动打开中的解决方案时[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 可在下列路径找到的工具和详细的指导文档：  
  
 **%Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**  
  
## <a name="before-you-migrate-your-dsl-projects"></a>将 DSL 项目的迁移之前  
 迁移工具修改[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]项目文件 (**.csproj**) 和解决方案文件 (**.sln**)。  
  
#### <a name="to-prepare-projects-for-migration"></a>若要准备迁移项目。  
  
- 请确保 **.csproj**并 **.sln**可以写入文件。 如果它们是受源代码管理，请确保在签出。  
  
- 制作一份你想要迁移的文件夹。  
  
## <a name="migrating-a-collection-of-projects"></a>迁移项目的集合  
  
#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>若要将 DSL 项目和解决方案迁移到 Visual Studio 2010  
  
1. 启动 DSL 迁移工具。  
  
   - 可以双击 Windows 资源管理器 （或文件资源管理器） 中的工具或命令提示符下启动该工具。 该工具位于以下位置：  
  
        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**  
  
2. 选择包含解决方案和你想要转换的项目的文件夹。  
  
   - 在工具，顶部的框中输入的路径或单击**浏览**。  
  
     迁移工具显示的定义，或使用 Dsl 项目的树。 在树中包括使用每个项目**Microsoft.VisualStudio.Modeling.Sdk**或**TextTemplating**程序集。  
  
3. 查看树中的项目，并取消选中不想要转换的项目。  
  
   - 选择项目或解决方案，以查看该工具将做的更改的列表。  
  
       > [!NOTE]
       > 显示文件夹名称旁边的复选框没有任何影响。 必须展开要检查项目和解决方案的文件夹。  
  
4. 转换项目。  
  
   1. 单击**转换**。  
  
        每个项目文件转换，一份之前_项目_**.csproj**另存为_项目_**。 vs2008.csproj**  
  
        每个副本_解决方案_**.sln**另存为_解决方案_**。 vs2008.sln**  
  
   2. 调查报告任何失败的转换。  
  
        在文本窗口中报告故障。 此外，树视图可以显示一个红色标志，未能转换每个节点上。 可以单击要获取有关该故障的详细信息的节点。  
  
5. **转换所有模板**解决方案中包含已成功转换项目。  
  
   1. 打开的解决方案。  
  
   2. 单击**转换所有模板**解决方案资源管理器的标头中的按钮。  
  
       > [!NOTE]
       > 您可以进行此步骤不必要。 有关详细信息，请参阅[如何自动执行转换所有模板](https://msdn.microsoft.com/b63cfe20-fe5e-47cc-9506-59b29bca768a)。  
  
6. 更新自定义代码，在转换后的项目中。  
  
   - 尝试生成项目，并调查任何故障。  
  
   - 测试您的设计器。  
  
## <a name="see-also"></a>请参阅  
 [可视化和建模 SDK 中的新增功能](../misc/what-s-new-in-visualization-and-modeling-sdk.md)
