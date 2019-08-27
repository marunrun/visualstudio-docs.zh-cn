---
title: 用于管理部署项目配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project configurations, managing deployment
- projects [Visual Studio SDK], configuration for managing deployment
ms.assetid: bd5940d9-d94d-4944-beda-4ec1ab2bbde5
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d5b16c3392e9432ba540130d45f6907de15b51ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429946"
---
# <a name="project-configuration-for-managing-deployment"></a>用于管理部署的项目配置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

部署是以物理方式将输出项的生成过程从移动到预期位置用于调试和安装的行为。 例如，Web 应用程序可能会在本地计算机上生成，然后放在服务器上。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 支持两种方法可以在部署中涉及的项目：  
  
- 作为部署过程的主题。  
  
- 作为部署过程的管理器。  
  
  可以部署解决方案之前，必须首先添加一个部署项目来配置部署选项。 如果尚不存在部署项目，会要求你想要选择时创建一个**部署解决方案**从**生成**菜单或右键单击该解决方案。 单击**是**会打开**添加新项目**带有对话框**远程部署向导**所选项目。  
  
  远程部署向导会要求你的应用程序 （Windows 或 Web） 的类型、 要包括的项目输出组、 要包括，任何其他文件和你想要将部署到远程计算机。 在向导的最后一页显示所选选项的摘要。  
  
  部署过程的使用者的项目生成输出项，必须将移动到备用的环境。 这些输出作为参数的说明项<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>接口，其主要用途如果以允许到组的输出的项目。 有关实现的详细信息`IVsProjectCfg2`，请参阅[用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。  
  
  部署项目，管理部署过程，启用部署命令和响应时选择此命令。 部署项目实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>界面，用于执行部署和调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback>接口的报表部署状态事件。  
  
  配置可指定对其生成或部署操作影响的依赖关系。 生成或部署的依赖项是必须为生成或部署之前或之后配置本身，生成或部署的项目。 描述项目之间建立依赖关系都<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency>接口，并部署使用的依赖项<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency>接口。 有关详细信息，请参阅[构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)。  
  
## <a name="see-also"></a>请参阅  
 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)   
 [用于构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)   
 [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
