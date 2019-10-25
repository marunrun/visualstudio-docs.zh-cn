---
title: 用于生成的项目配置 |Microsoft Docs
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
ms.openlocfilehash: 956449d1207a9831f9dd04a707fffe4b9b5a4221
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726048"
---
# <a name="project-configuration-for-building"></a>用于生成的项目配置
给定解决方案的解决方案配置列表由 "解决方案配置" 对话框管理。

 用户可以创建其他解决方案配置，每个配置都具有自己的唯一名称。 当用户创建新的解决方案配置时，IDE 默认为项目中的相应配置名称; 如果不存在相应的名称，则为 Debug。 必要时，用户可以更改所选内容以满足特定要求。 此行为的唯一例外是当项目支持与新解决方案配置的名称相匹配的配置时。 例如，假设解决方案包含 Project1 和 Project2。 Project1 具有 "调试"、"零售" 和 "MyConfig1" 的项目配置。 Project2 具有 "调试"、"零售" 和 "MyConfig2" 的项目配置。

 如果用户创建名为 MyConfig2 的新解决方案配置，则默认情况下，Project1 将其调试配置绑定到解决方案配置。 默认情况下，Project2 还会将其 MyConfig2 配置绑定到解决方案配置。

> [!NOTE]
> 绑定不区分大小写。

 当用户在 "配置" 下拉列表中选择 "**多选择**" 项时，环境会显示一个对话框，其中提供了可用配置的列表。

 ![多个配置](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs")多个配置

 在此对话框中，用户可以选择一个或多个配置。 选择后，"属性页" 对话框中显示的属性值将反映所选配置的值的交集。

 有关添加和重命名解决方案和项目的配置的信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

 项目依赖项和生成顺序独立于解决方案配置：也就是说，对于解决方案中的所有项目，只能设置一个依赖项树。 右键单击解决方案或项目，然后选择 "**项目依赖项**" 或 "**项目生成顺序**" 选项，打开 "**项目依赖项**" 对话框。 也可以从 "**项目**" 菜单中打开它。

 ![项目依赖项](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies")项目依赖项

 项目依赖项决定项目生成的顺序。 使用对话框中的 "生成顺序" 选项卡可以查看解决方案中项目的生成顺序，并使用 "依赖项" 选项卡修改生成顺序。

> [!NOTE]
> 由于 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> 接口指定的显式依赖项，已在列表中选择了复选框但显示为灰色的项目，因为它是由或接口指定的显式依赖项，因此无法更改。 例如，将 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目中的项目引用添加到另一个项目会自动添加一个生成依赖项，该依赖项只能通过删除引用来删除。 不能选择其复选框处于清除状态并灰显的项目，因为这样做会创建一个依赖项循环（例如，Project1 依赖于 Project2，而 Project2 依赖于 Project1），这会使生成延迟。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 生成过程包括使用单个生成命令调用的典型编译和链接操作。 还可以支持两个其他生成过程：一个用于删除上一生成的所有输出项的干净操作，以及一个最新的检查，以确定配置中的输出项是否已更改。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 对象将返回相应的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> （从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A> 返回）以管理它们的生成过程。 若要在生成操作发生时报告生成操作的状态，配置将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback>，由环境实现的接口和对生成状态事件感兴趣的任何其他对象调用。

 构建后，可以使用配置设置来确定是否可以在调试器的控制下运行这些设置。 配置实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> 以支持调试。

 实现项目依赖项后，可以通过自动化模型以编程方式操作依赖项。 在自动化模型中调用 <xref:EnvDTE.SolutionBuild.BuildDependencies%2A>。 没有允许直接操作解决方案生成管理器配置及其属性的 VSIP API 级接口。

 此外，您可以在 "项目依赖项" 窗口中提供网格。 有关详细信息，请参阅[属性显示网格](../../extensibility/internals/properties-display-grid.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于管理部署的项目配置](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)