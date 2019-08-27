---
title: 注意事项卸载并重新加载嵌套项目 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197003"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>卸载和重新加载嵌套项目的注意事项
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

实现嵌套的项目类型时，你必须卸载并重新加载项目时执行附加步骤。 若要正确通知解决方案的事件侦听器，必须正确引发`OnBeforeUnloadProject`和`OnAfterLoadProject`事件。  
  
 您必须引发这些事件以这种方式的一个原因是不希望源代码管理 (SCC) 以从服务器中删除项，然后将其添加为新内容，如果没有`Get`从源代码管理操作。 在这种情况下，将从源代码管理中加载的新文件，您必须卸载并重新加载所有文件，以防它们是不同的。 SCC 调用`ReloadItem`。 该调用的实现是删除项目，然后重新创建再次通过实现`IVsFireSolutionEvents`来调用`OnBeforeUnloadProject`和`OnAfterLoadProject`。 当你执行此实现时，SCC 将得到通知，已暂时删除并再次添加该项目。 因此，SCC 不会不运行该项目时项目已实际从服务器中删除，然后再次添加。  
  
## <a name="reloading-projects"></a>重新加载项目  
 若要支持重新加载嵌套项目的则实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>方法。 实现中`ReloadItem`，关闭嵌套的项目，然后再重新创建它们。  
  
 通常当重新加载项目时，IDE 将引发<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A>和`M:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject(Microsoft.VisualStudio.Shell.Interop.IVsHierarchy,Microsoft.VisualStudio.Shell.Interop.IVsHierarchy)`事件。 但是，对于将删除并重新加载嵌套项目，父项目启动过程中，不在 IDE。 因为父项目不会引发解决方案事件和 IDE 提供有关初始化过程的任何信息，不会引发事件。  
  
 若要处理此过程中，父项目调用`QueryInterface`上<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents>关闭接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution>接口。 `IVsFireSolutionEvents` 具有函数告知 IDE 引发`OnBeforeUnloadProject`事件以卸载嵌套的项目，然后引发`OnAfterLoadProject`事件来重新加载同一个项目。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>   
 [嵌套项目](../../extensibility/internals/nesting-projects.md)
