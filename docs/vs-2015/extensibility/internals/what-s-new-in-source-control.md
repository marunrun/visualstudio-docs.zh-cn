---
title: 源代码管理中的新增功能
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 31b55c57f47f25814eff24f13bcf91408468d0f4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200955"
---
# <a name="what39s-new-in-source-control-in-visual-studio-2015"></a>Visual Studio 2015 的源代码管理中的新增功能&#39;

[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在中 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] ，可以通过实现源控件 VSPackage，提供深度集成的源代码管理解决方案。 本部分介绍源代码管理 Vspackage 的功能，并概述实现步骤。  
  
## <a name="the-source-control-vspackage"></a>源代码管理 VSPackage  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 支持两种类型的源代码管理解决方案。 在的所有版本中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，你仍然可以集成源代码管理插件基于 API 的插件。 你还可以为源代码管理创建 VSPackage，它提供了一个 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 适用于需要高级别复杂和自治的源代码管理解决方案的深度集成。  
  
 VSPackage 可向添加几乎任何类型的功能 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 源代码管理 VSPackage 为提供了一个完整的源代码管理功能 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，即从向用户显示的 UI 到与源代码管理系统的后端通信。  
  
 实现源代码管理 VSPackage 需要 "全部或无" 策略。 源代码管理 VSPackage 的创建者必须投入大量精力来实现一些源代码管理接口和新的 UI 元素 (对话框、菜单和工具栏) ，以涵盖整个源代码管理功能，以及任何要成功集成的包所需的接口 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 以下步骤概述了实现源代码管理包所需的操作。 有关详细信息，请参阅 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)。  
  
1. 创建提供专用源代码管理服务的 VSPackage。  
  
2. 实现 (提供的源代码管理相关服务中的接口 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，例如， <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> 接口) 。  
  
3. 注册源代码管理 VSPackage。  
  
4. 实现所有源代码管理 UI，包括菜单项、对话框、工具栏和上下文菜单。  
  
5. 当事件处于活动状态且必须由 VSPackage 处理时，所有与源代码管理相关的事件均会传递到源代码管理 VSackage。  
  
6. 源代码管理 VSPackage 必须侦听事件（例如实现接口的事件）， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> 并跟踪项目文档 (TPD) 事件 (由 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 接口) 实现并执行必要的操作。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>   
 [叙述](../../extensibility/internals/source-control-integration-overview.md)   
 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
