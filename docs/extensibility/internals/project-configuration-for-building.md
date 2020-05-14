---
title: 建筑项目配置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bdd084053e06206a99298b234b4d51c8504119a2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706730"
---
# <a name="project-configuration-for-building"></a>用于生成的项目配置
给定解决方案的解决方案配置列表由"解决方案配置"对话框管理。

 用户可以创建其他解决方案配置，每个配置都有自己的唯一名称。 当用户创建新的解决方案配置时，IDE 默认为项目中的相应配置名称，如果不存在相应的名称，则"调试"。 如有必要，用户可以更改所选内容以满足特定要求。 此行为的唯一例外是项目支持与新解决方案配置名称匹配的配置。 例如，假设解决方案包含 Project1 和 Project2。 Project1 具有项目配置调试、零售和 MyConfig1。 Project2 具有项目配置调试、零售和 MyConfig2。

 如果用户创建了名为 MyConfig2 的新解决方案配置，Project1 默认情况下将其调试配置绑定到解决方案配置。 默认情况下，Project2 还将其 MyConfig2 配置绑定到解决方案配置。

> [!NOTE]
> 绑定不区分大小写。

 当用户在配置下拉列表中选择 **"多个选择**"项时，环境将显示一个对话框，提供可用配置的列表。

 ![多种配置](../../extensibility/internals/media/vsmultiplecfgs.gif "vs 多倍Cfgs")多种配置

 在此对话框中，用户可以选择一个或多个配置。 选中后，属性页对话框中显示的属性值将反映所选配置的值的交集。

 有关添加和重命名解决方案和项目的配置的信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

 项目依赖项和生成顺序与解决方案配置无关：也就是说，只能为解决方案中的所有项目设置一个依赖项树。 右键单击解决方案或项目并选择"**项目依赖项**"或 **"项目生成订单"** 选项将打开 **"项目依赖项"** 对话框。 也可以从 **"项目"** 菜单打开它。

 ![项目依赖项](../../extensibility/internals/media/vsprojdependencies.gif "vsProj 依赖")项目依赖项

 项目依赖项确定项目生成的顺序。 使用对话框上的"生成订单"选项卡查看解决方案中项目生成的确切顺序，并使用"依赖项"选项卡修改生成顺序。

> [!NOTE]
> 由于 或<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency><xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency>接口指定的显式依赖项，环境已添加列表中选中其复选框但显示为变暗的项目，并且无法更改。 例如，将项目引用添加到另一[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]个项目会自动添加只能通过删除引用删除的生成依赖项。 无法选择复选框清晰且显示为变暗的项目，因为这样做将创建依赖项循环（例如，Project1 将依赖于 Project2，Project2 将依赖于 Project1），这将阻止生成。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]生成过程包括使用单个 Build 命令调用的典型编译和链接操作。 还可以支持另外两个生成过程：从上一个生成中删除所有输出项的干净操作，以及确定配置中的输出项是否已更改的最新检查。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>对象返回相应的<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>（从<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>返回）来管理其生成过程。 要报告生成操作发生时的状态，配置将<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback>调用 ，环境与对生成状态事件感兴趣的任何其他对象实现的接口。

 生成配置设置后，可以使用 这些设置来确定它们是否可以在调试器的控制下运行。 支持调试的<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>配置实现。

 实现项目依赖项后，可以通过自动化模型以编程方式操作依赖项。 在自动化<xref:EnvDTE.SolutionBuild.BuildDependencies%2A>模型中调用。 没有可用的 VSIP API 级接口允许直接操作解决方案生成管理器配置及其属性。

 此外，您可以在项目依赖项窗口中提供网格。 有关详细信息，请参阅[属性显示网格](../../extensibility/internals/properties-display-grid.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于管理部署的项目配置](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
