---
title: 卸载和重新加载嵌套项目
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 86f8f2f02258bc55f3221635fddab8ecdaaa3cf7
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89743240"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>卸载和重新加载嵌套项目的注意事项

当您实现嵌套项目类型时，您必须在卸载和重新加载项目时执行其他步骤。 若要正确地将侦听器通知给解决方案事件，必须正确地引发 `OnBeforeUnloadProject` 和 `OnAfterLoadProject` 事件。

引发这些事件的一个原因是 (SCC) 的源代码管理。 您不希望 SCC 从服务器中删除这些项目，然后将它们作为 *新* 文件添加，如果有 `Get` 来自 SCC 的操作。 在这种情况下，会将新文件从 SCC 中加载。 如果文件不同，则必须卸载并重新加载所有文件。

源代码管理调用 `ReloadItem` 。 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> 接口以调用 `OnBeforeUnloadProject` 并 `OnAfterLoadProject` 重新创建项目。 以这种方式实现接口时，会通知 SCC 系统临时删除并再次添加该项目。 因此，SCC 不会对项目进行操作，就像 *实际* 删除并重新添加项目一样。

## <a name="reload-projects"></a>重新加载项目

若要支持加载嵌套项目，需要实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> 方法。 在的实现中 `ReloadItem` ，关闭嵌套的项目，然后重新创建它们。

通常，当重新加载项目时，IDE 将引发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> 事件。 但是，对于删除和重新加载的嵌套项目，父项目将启动进程，而不是 IDE。 因为父项目不会引发解决方案事件，并且 IDE 没有与进程初始化相关的信息，因此不会引发事件。

若要处理此进程，父项目将 `QueryInterface` 在接口上调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> 。 `IVsFireSolutionEvents` 具有指示 IDE 引发 `OnBeforeUnloadProject` 事件以卸载嵌套项目的函数，并引发 `OnAfterLoadProject` 事件以重新加载同一项目。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
