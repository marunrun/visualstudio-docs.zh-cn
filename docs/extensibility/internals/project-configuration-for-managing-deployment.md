---
title: 用于管理部署的项目配置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, managing deployment
- projects [Visual Studio SDK], configuration for managing deployment
ms.assetid: bd5940d9-d94d-4944-beda-4ec1ab2bbde5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62f7bf6535a89e46799ade88fe8976974b3019c5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706701"
---
# <a name="project-configuration-for-managing-deployment"></a>用于管理部署的项目配置
部署是物理将输出项从生成过程移动到用于调试和安装的预期位置的行为。 例如，Web 应用程序可能构建在本地计算机上，然后放置在服务器上。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持项目参与部署的两种方式：

- 作为部署过程的主题。

- 作为部署过程的经理。

  在部署解决方案之前，必须首先添加部署项目以配置部署选项。 如果部署项目不存在，当您从 **"生成**"菜单中选择 **"部署解决方案"** 或右键单击解决方案时，系统会询问您是否要创建一个部署项目。 单击 **"是**"将打开"**添加新项目**"对话框，并选择 **"远程部署向导"** 项目。

  远程部署向导要求您提供应用程序类型（Windows 或 Web）、要包括的项目输出组、要包括的任何其他文件以及要部署到的远程计算机。 向导的最后一页显示所选选项的摘要。

  作为部署过程主题的项目将生成必须移动到备用环境的输出项。 这些输出项被描述为接口的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>参数，如果允许项目对输出进行分组，则接口的主要目的是这些参数。 有关 实现`IVsProjectCfg2`的详细信息，请参阅[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。

  管理部署过程的部署项目启用"部署"命令并在选择此命令时响应。 部署项目实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>该接口以执行部署，并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback>该接口以报告部署状态事件。

  配置可以指定影响其生成或部署操作的依赖项。 生成或部署依赖项是必须在构建或部署配置之前或之后生成或部署的项目。 使用接口描述项目之间的生成依赖关系，<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency>并部署使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency>接口的依赖项。 有关详细信息，请参阅[用于构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
