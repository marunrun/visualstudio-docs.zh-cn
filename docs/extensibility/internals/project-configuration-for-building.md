---
title: 项目生成配置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fd9464105d777c0d488175ad67e1481022caa2d1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328540"
---
# <a name="project-configuration-for-building"></a>用于生成的项目配置
解决方案配置对话框中由托管给定解决方案的解决方案配置的列表。

 用户可以创建其他解决方案配置，每个都有其自己唯一的名称。 当用户创建新的解决方案配置时，IDE 将默认为项目中或调试中的相应配置名称如果存在没有相应的名称。 用户可以更改所选内容以满足特定要求，如有必要。 项目支持与新解决方案配置的名称相匹配的配置时，此行为的唯一例外。 例如，假设一种解决方案包含 Project1 和 Project2。 Project1 具有调试、 零售版和 MyConfig1 项目配置。 Project2 具有调试、 零售版和 MyConfig2 项目配置。

 如果用户创建新的解决方案配置名为 MyConfig2，Project1 其调试配置的解决方案配置为默认情况下绑定。 Project2 还将绑定其 MyConfig2 配置到解决方案配置默认情况下。

> [!NOTE]
> 绑定是不区分大小写。

 当用户选择**多个所选内容**项在配置下拉列表中，环境将显示一个对话框，提供了可用的配置的列表。

 ![多个配置](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs")多个配置

 在此对话框中，用户可以选择一个或多个配置。 选择后，在属性页对话框上显示的属性值将反映所选配置的值的交集。

 请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)有关添加和重命名解决方案和项目的配置相关的信息。

 项目依赖项和生成顺序是独立的解决方案配置： 也就是说，您只能设置为所有解决方案中项目的一个依赖关系树。 右键单击该解决方案或项目，然后选择**项目依赖项**或**项目生成顺序**选项将打开**项目依赖项**对话框。 也可以从打开**项目**菜单。

 ![项目依赖项](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies")项目依赖项

 项目依赖项确定在其中生成项目的顺序。 若要查看解决方案中的项目将生成，并使用依赖关系选项卡来修改生成顺序的确切顺序，请使用对话框的生成顺序选项卡。

> [!NOTE]
> 已添加的环境，因为指定的显式依赖关系列表中的项目已选中其复选框，但显示为灰色<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency>接口，并且不能更改。 例如，添加项目引用从[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]到另一个项目的项目会自动添加仅可以通过删除引用删除的生成依赖项。 不能选择的项目的复选框清晰，并显示为灰色，因为执行此操作会在创建依赖关系循环 （例如，Project1 是依赖于 Project2，和将依赖于 Project1 Project2），这会停止生成。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 生成过程包括典型的编译和链接操作调用的单个生成命令。 也可以支持两个其他生成过程： 从之前的版本和最新检查以确定是否已更改配置中的输出项中删除所有输出项的清理操作。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 对象返回的相应<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>(从返回<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>) 来管理其生成过程。 若要报告生成操作的状态，正在进行中时，配置使调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback>、 接口实现的环境和任何其他对象是否有兴趣生成状态事件。

 生成后，配置设置可以用于确定可以运行这些受调试器控制。 配置实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>以支持调试。

 实现项目依赖项之后, 可以以编程方式操作通过自动化模型的依赖项。 在调用<xref:EnvDTE.SolutionBuild.BuildDependencies%2A>自动化模型中。 没有可用 VSIP API 级别接口，允许直接解决方案生成管理器配置及其属性的操作。

 此外，您可以提供项目依赖项窗口中的一个网格。 有关详细信息，请参阅[属性显示网格](../../extensibility/internals/properties-display-grid.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于管理部署的项目配置](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)