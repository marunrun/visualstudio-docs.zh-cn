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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698688"
---
# <a name="upgrading-project-items"></a>升级项目项
如果您添加或管理不实现项目系统内的项，您可能需要参与项目升级过程。 Crystal Reports 是项的可以添加到项目系统的示例。  
  
 通常情况下，项目项实施者想要利用已完全实例化和升级项目，因为它们需要知道哪些项目的引用和其他项目属性还有哪些做出升级的决策。  
  
### <a name="to-get-the-project-upgrade-notification"></a>若要获取项目升级通知  
  
1. 设置<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80.SolutionOrProjectUpgrading>中您的项目项实现 （vsshell80.idl 中定义） 的标志。 这会导致您的项目项 VSPackage 自动加载时[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]shell 确定在升级过程中为项目系统。  
  
2. 建议<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade>接口通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution2.AdviseSolutionEvents%2A>方法。  
  
3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade>接口项目系统实现完成其升级操作并创建新升级后的项目后触发。 此方案中，根据<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade>接口触发后<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A>，则<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>，或<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A>方法。  
  
### <a name="to-upgrade-the-project-item-files"></a>若要升级项目项文件  
  
1. 在项目项实现中，您必须仔细管理文件备份过程。 这尤其适用于通过并行备份，其中`fUpgradeFlag`的参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A>方法设置为<xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS>，沿指定为".old"标记的端文件已备份的文件的放置位置。 早于该项目已升级时的系统时间的备份的文件可指定为已过时。 此外，它们可能会覆盖除非采取特定步骤来防止这种情况。  
  
2. 在时您的项目项获取的项目升级时，通知**Visual Studio 转换向导**仍然会显示。 因此，应使用的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger>接口，以提供对向导用户界面升级的消息。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 转换向导](https://msdn.microsoft.com/4acfd30e-c192-4184-a86f-2da5e4c3d83c)   
 [升级自定义项目](../misc/upgrading-custom-projects.md)