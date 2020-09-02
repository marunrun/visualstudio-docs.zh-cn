---
title: 解决方案配置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solution configurations
ms.assetid: f22cfc75-3e31-4e0d-88a9-3ca99539203b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7c96b73747ef8b136a74a7256cde7fef8d1c42de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705380"
---
# <a name="solution-configuration"></a>解决方案配置
解决方案配置存储解决方案级属性。 它们定向 **开始** (F5) 键和 **生成** 命令的行为。 默认情况下，这些命令生成并启动调试配置。 这两个命令都在解决方案配置的上下文中执行。 这意味着，用户可能希望按 F5 启动并生成通过设置配置的任何活动解决方案。 环境旨在针对解决方案而不是在生成和运行时进行优化。

 标准 Visual Studio 工具栏包含开始按钮右侧的 "开始" 按钮和 "解决方案配置" 下拉按钮。 此列表允许用户选择按下 F5 时要启动的配置，创建自己的解决方案配置，或编辑现有配置。

> [!NOTE]
> 没有可扩展性接口，无法创建或编辑解决方案配置。 您必须使用 `DTE.SolutionBuild`。 但是，有一些可扩展性 Api 用于管理解决方案生成。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>。

 下面介绍如何实现项目类型支持的解决方案配置：

- 项目

   显示在当前解决方案中找到的项目的名称。

- 配置

   若要提供项目类型支持的配置列表并显示在属性页中，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 。

   "配置" 列显示要在此解决方案配置中生成的项目配置的名称，并在单击箭头按钮时列出所有项目配置。 环境调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A> 方法来填充此列表。 如果该 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> 方法指示项目支持配置编辑，则 "配置" 标题下也会显示 "新建" 或 "编辑" 选项。 其中每个选择都将启动调用接口的方法的对话框， `IVsCfgProvider2` 以编辑项目的配置。

   如果项目不支持配置，则 "配置" 列将显示 "无" 且被禁用。

- 平台

   显示所选项目配置的生成平台，并在单击箭头按钮时列出项目的所有可用平台。 环境调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A> 方法来填充此列表。 如果该 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> 方法指示项目支持平台编辑，则 "平台" 标题下也会显示 "新建" 或 "编辑" 选项。 其中每个选择都将启动对话框，这些对话框调用 `IVsCfgProvider2` 方法来编辑项目的可用平台。

   如果项目不支持平台，则该项目的 "平台" 列将显示 "无" 且被禁用。

- 构建

   指定项目是否由当前解决方案配置生成。 如果未选择的项目包含任何项目依赖项，则将不生成这些项目。 在调试、运行、打包和部署解决方案时，仍未选择要生成的项目。

- 部署

   指定在将启动或部署命令用于选定的解决方案生成配置时是否部署项目。 如果项目支持通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 在其对象上实现接口来进行部署，则此字段的复选框将可用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 。

  添加新的解决方案配置后，用户可以从 "标准" 工具栏上的 "解决方案配置" 下拉列表框中选择它以生成和/或启动该配置。

## <a name="see-also"></a>另请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
