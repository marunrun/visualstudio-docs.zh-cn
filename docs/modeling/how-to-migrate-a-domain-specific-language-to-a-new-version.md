---
title: 如何：将域特定语言迁移至新版本
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 63d313534fab789c5e4e79fb644111314e054250
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445150"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>如何：将域特定语言迁移至新版本
你可以迁移项目的定义和使用特定于域的语言设置为[!INCLUDE[vs2010](../misc/includes/vs2010_md.md)]的版本从[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]一起分发[!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)]。

 作为的一部分提供迁移工具[!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)]。 工具将为 Visual Studio 项目和解决方案的使用或定义 DSL 工具。

 您必须显式运行迁移工具： 它就不会启动自动在 Visual Studio 中打开解决方案时。 可在下列路径找到的工具和详细的指导文档：

 **%Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>将 DSL 项目的迁移之前
 迁移工具修改 Visual Studio 项目文件 (**.csproj**) 和解决方案文件 (**.sln**)。

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
       > 您可以进行此步骤不必要。 有关详细信息，请参阅[如何自动执行转换所有模板](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))。

6. 更新自定义代码，在转换后的项目中。

   - 尝试生成项目，并调查任何故障。

   - 测试您的设计器。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)