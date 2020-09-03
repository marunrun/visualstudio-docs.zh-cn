---
title: 卸载和重新加载嵌套项目的注意事项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65145530c8cd6b68b82391a09b395bb8c9a61117
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197003"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>卸载和重新加载嵌套项目的注意事项
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当您实现嵌套项目类型时，您必须在卸载和重新加载项目时执行其他步骤。 若要正确地将侦听器通知给解决方案事件，必须正确地引发 `OnBeforeUnloadProject` 和 `OnAfterLoadProject` 事件。  
  
 您必须以这种方式引发这些事件的一个原因是您不希望源代码管理 (SCC) 从服务器中删除这些项，然后将这些项作为新内容添加回，如果存在 `Get` 来自 SCC 的操作。 在这种情况下，会将新文件加载到 SCC 外，并且必须卸载和重载所有文件，以防它们不同。 SCC 调用 `ReloadItem` 。 此调用的实现是删除项目，并通过实现调用和重新创建它 `IVsFireSolutionEvents` `OnBeforeUnloadProject` `OnAfterLoadProject` 。 当你执行此实现时，将通知 SCC 已暂时删除并再次添加该项目。 因此，SCC 不会对项目进行操作，就像实际上是从服务器中删除了项目，然后再次添加该项目一样。  
  
## <a name="reloading-projects"></a>重新加载项目  
 若要支持加载嵌套项目，需要实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> 方法。 在的实现中 `ReloadItem` ，关闭嵌套的项目，然后重新创建它们。  
  
 通常，当重新加载项目时，IDE 将引发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A> 和 `M:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject(Microsoft.VisualStudio.Shell.Interop.IVsHierarchy,Microsoft.VisualStudio.Shell.Interop.IVsHierarchy)` 事件。 但是，对于将被删除和重新加载的嵌套项目，父项目将启动进程，而不是 IDE。 因为父项目不会引发解决方案事件，并且 IDE 没有与进程初始化相关的信息，因此不会引发事件。  
  
 若要处理此进程，父项目将 `QueryInterface` 在接口上调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> 。 `IVsFireSolutionEvents` 具有指示 IDE 引发 `OnBeforeUnloadProject` 事件以卸载嵌套项目的函数，并引发 `OnAfterLoadProject` 事件以重新加载同一项目。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>   
 [嵌套项目](../../extensibility/internals/nesting-projects.md)
