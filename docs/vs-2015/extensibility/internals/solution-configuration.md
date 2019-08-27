---
title: 解决方案配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solution configurations
ms.assetid: f22cfc75-3e31-4e0d-88a9-3ca99539203b
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bbd47969a7a48be817e8e2f5359705e03b5d0dc2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432094"
---
# <a name="solution-configuration"></a>解决方案配置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

解决方案配置存储解决方案级别的属性。 它们指示的行为**启动**(f5) 和**生成**命令。 默认情况下，这些命令生成并启动调试配置。 在解决方案配置的上下文中执行这两个命令。 这意味着用户可以启动和任何活动解决方案配置通过设置生成预期 F5。 在环境旨在构建和运行时优化解决方案而不是项目。  
  
 标准 Visual Studio 工具栏中包含开始按钮和一个解决方案配置下拉列表右侧的开始按钮。 此列表，用户可以选择按下 F5 时要启动的配置、 创建其自己的解决方案配置，或编辑现有配置。  
  
> [!NOTE]
> 没有可扩展性接口来创建或编辑解决方案配置。 必须使用`DTE.SolutionBuilder`。 但是，有用于管理解决方案生成的可扩展 Api。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>。  
  
 下面是如何实现您的项目类型支持的解决方案配置：  
  
- 项目  
  
   显示在当前解决方案中找到的项目的名称。  
  
- 配置  
  
   若要提供的配置项目类型支持的列表，显示在属性页中，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>。  
  
   配置列显示的要在此解决方案配置中，生成的项目配置名称，并单击箭头按钮时列出的所有项目配置。 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A>方法来填充此列表。 如果<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A>方法指示项目支持编辑配置，新建或编辑的选择也会显示在配置标题下。 这些选择的每个启动调用的方法的对话框`IVsCfgProvider2`接口来编辑项目的配置。  
  
   如果项目不支持的配置，配置列显示无且被禁用。  
  
- Platform  
  
   显示选定的项目配置生成，并单击箭头按钮时列出所有可用的平台的项目的平台。 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A>方法来填充此列表。 如果<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A>方法指示项目支持编辑平台，新建或编辑的选择也会显示在平台标题下。 这些选择的每个启动调用的对话框`IVsCfgProvider2`方法来编辑项目的可用平台。  
  
   如果项目不支持的平台，该项目的平台列显示无且被禁用。  
  
- Build  
  
   指定由当前的解决方案配置生成项目。 尽管它们所包含任何项目依赖项调用解决方案级生成命令时不生成未选定的项目。 未选定要生成的项目仍包含在调试、 运行、 打包和部署解决方案中。  
  
- 部署  
  
   指定的开始或部署命令使用具有所选的解决方案生成配置时将部署项目。 此字段的复选框将提供如果项目支持部署通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>接口及其<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>对象。  
  
  后添加新的解决方案配置，用户可以选择从标准工具栏以生成和/或启动该配置的解决方案配置下拉列表框。  
  
## <a name="see-also"></a>请参阅  
 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)   
 [用于构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)   
 [项目配置对象](../../extensibility/internals/project-configuration-object.md)
