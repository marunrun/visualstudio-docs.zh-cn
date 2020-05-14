---
title: 解决方案配置 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705380"
---
# <a name="solution-configuration"></a>解决方案配置
解决方案配置存储解决方案级属性。 它们指示**开始**（F5） 键和**生成**命令的行为。 默认情况下，这些命令生成并启动调试配置。 这两个命令都在解决方案配置的上下文中执行。 这意味着用户可以期望 F5 启动和生成通过设置配置的活动解决方案的任何内容。 该环境旨在优化解决方案，而不是项目，当涉及到构建和运行。

 标准 Visual Studio 工具栏包含"开始"按钮和"开始"按钮右侧的解决方案配置下拉。 此列表允许用户选择在按下 F5 时启动的配置、创建自己的解决方案配置或编辑现有配置。

> [!NOTE]
> 没有可扩展接口来创建或编辑解决方案配置。 您必须使用 `DTE.SolutionBuild`。 但是，存在用于管理解决方案构建的可扩展性 API。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>。

 以下是实现项目类型支持的解决方案配置的方式：

- Project

   显示当前解决方案中找到的项目名称。

- 配置

   要提供项目类型支持并在属性页中显示的配置列表，请实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>。

   "配置"列显示要在此解决方案配置中生成的项目配置的名称，并在单击箭头按钮时列出所有项目配置。 环境调用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A>以填写此列表。 如果<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A>方法指示项目支持配置编辑，则"新建"或"编辑"选择也会显示在"配置"标题下。 每个选择都会启动对话框，这些对话框调用`IVsCfgProvider2`接口的方法来编辑项目的配置。

   如果项目不支持配置，则"配置"列将显示"无"并禁用。

- 平台

   显示所选项目配置生成的平台，并在单击箭头按钮时列出项目的所有可用平台。 环境调用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A>以填写此列表。 如果<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A>方法指示项目支持平台编辑，则"新建"或"编辑"选择也会显示在"平台"标题下。 每个选择都会启动对话框，这些对话框调用`IVsCfgProvider2`方法来编辑项目的可用平台。

   如果项目不支持平台，该项目的平台列将显示"无"并禁用。

- 生成

   指定项目是否由当前解决方案配置生成。 调用解决方案级生成命令时，即使其中包含任何项目依赖项，则不会生成未选择的项目。 未选择要生成的项目仍包含在解决方案的调试、运行、打包和部署中。

- 部署

   指定在"开始"或"部署"命令与所选解决方案生成配置一起使用时，是否将部署项目。 如果项目支持通过在其<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg><xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>对象上实现接口来部署，则此字段的复选框将可用。

  添加新解决方案配置后，用户可以从标准工具栏上的"解决方案配置"下拉列表框中选择它，以生成和/或启动该配置。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
