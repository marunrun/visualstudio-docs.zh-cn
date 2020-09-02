---
title: 升级项目项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- upgrading project items
- projects [Visual Studio SDK], upgrading items
- project items [Visual Studio], upgrading
ms.assetid: 8af29dd4-eaf1-4b3c-b602-198e1a3dff23
caps.latest.revision: 14
manager: jillfra
ms.openlocfilehash: eb3619e187c7856cf03ee60c8a04cbe527bf0a69
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65698688"
---
# <a name="upgrading-project-items"></a>升级项目项
如果在不实现的项目系统内添加或管理项，可能需要参与项目升级过程。 Crystal Reports 是可以添加到项目系统中的项的一个示例。  
  
 通常，项目项实施人员希望利用已经完全实例化和升级的项目，因为他们需要知道项目引用是什么，以及有哪些其他项目属性来做出升级决策。  
  
### <a name="to-get-the-project-upgrade-notification"></a>获取项目升级通知  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80.SolutionOrProjectUpgrading>在项目项实现中设置 vsshell80) 中定义 (标志。 当 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] shell 确定项目系统正在升级时，这会导致项目项 VSPackage 自动加载。  
  
2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade>通过方法通知接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution2.AdviseSolutionEvents%2A> 。  
  
3. 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> 项目系统实现完成其升级操作并创建新的已升级项目之后，将触发接口。 根据具体方案， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> 接口将在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> 或方法之后激发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> 。  
  
### <a name="to-upgrade-the-project-item-files"></a>升级项目项文件  
  
1. 你必须在项目项实现中仔细管理文件备份过程。 这种情况特别适用于并行备份，其中 `fUpgradeFlag` 方法的参数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 设置为 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> ，其中已备份的文件沿着指定为 ".old" 的侧文件放置。 在升级项目之前，备份的文件早于系统时间，可以指定为过时。 而且，它们可能会被覆盖，除非你采取特定的步骤来防止出现这种情况。  
  
2. 当项目项收到项目升级通知时，仍然会显示 **Visual Studio 转换向导** 。 因此，应使用接口的方法向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> 向导 UI 提供升级消息。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 转换向导](https://msdn.microsoft.com/4acfd30e-c192-4184-a86f-2da5e4c3d83c)   
 [升级自定义项目](../misc/upgrading-custom-projects.md)