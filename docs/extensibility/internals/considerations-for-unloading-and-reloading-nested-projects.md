---
title: 卸载和重新加载嵌套项目的注意事项 |微软文档
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
ms.openlocfilehash: 2ab705953eea1fcac99883bb4f88c0e95eced108
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709289"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>卸载和重新加载嵌套项目的注意事项

实现嵌套项目类型时，在卸载和重新加载项目时必须执行其他步骤。 要正确通知侦听器到解决方案事件，必须正确引发`OnBeforeUnloadProject``OnAfterLoadProject`和 事件。

引发这些事件的一个原因是源代码控制 （SCC）。 您不希望 SCC 从服务器中删除这些项目，然后将其添加为*新*项目（如果 SCC 中有操作`Get`）。 在这种情况下，将从 SCC 加载新文件。 您必须卸载并重新加载所有文件，以防它们不同。

源代码控制调用`ReloadItem`。 实现要<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents>调用`OnBeforeUnloadProject`的接口并`OnAfterLoadProject`删除项目并重新创建它。 以这种方式实现接口时，SCC 会被告知项目已暂时删除并再次添加。 因此，SCC 不会在项目上运行，就像*项目实际上*已被删除并重新添加一样。

## <a name="reload-projects"></a>重新加载项目

要支持重新加载嵌套项目，可以实现 该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>。 在实现 中`ReloadItem`，将关闭嵌套项目，然后重新创建这些项目。

通常，在重新加载项目时，IDE 会引发<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A>和 事件。 但是，对于删除并重新加载的嵌套项目，父项目将启动进程，而不是 IDE。 由于父项目不引发解决方案事件，并且 IDE 没有关于进程初始化的信息，因此不会引发这些事件。

要处理此过程，父项目调用`QueryInterface`<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents>接口。 `IVsFireSolutionEvents`具有告诉 IDE 引发`OnBeforeUnloadProject`事件以卸载嵌套项目，然后引发`OnAfterLoadProject`事件以重新加载同一项目的函数。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
