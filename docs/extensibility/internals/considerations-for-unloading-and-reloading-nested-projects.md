---
title: 注意事项卸载并重新加载嵌套项目 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0a45cf72f09ddf4e5ac1d68b59c2b13e64982744
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335544"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>有关卸载和重新加载嵌套的项目的注意事项

实现嵌套的项目类型时，你必须卸载并重新加载项目时执行附加步骤。 若要正确通知解决方案的事件侦听器，必须正确引发`OnBeforeUnloadProject`和`OnAfterLoadProject`事件。

若要引发这些事件的原因之一是进行源代码管理 (SCC)。 您不希望 SCC 从服务器中删除项，然后将它们添加回作为*新*是否存在`Get`从源代码管理操作。 在这种情况下，将超出 SCC 加载的新文件。 必须卸载并重新加载所有文件，以防它们之间的差异。

源代码控件调用`ReloadItem`。 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents>接口来调用`OnBeforeUnloadProject`和`OnAfterLoadProject`若要删除项目，然后重新创建它。 当以这种方式实现接口时，SCC 将得到通知，已暂时删除并再次添加该项目。 因此，SCC 就像该项目是不会运行该项目*实际上*删除并重新添加。

## <a name="reload-projects"></a>重新加载项目

若要支持重新加载嵌套项目的则实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>方法。 实现中`ReloadItem`，关闭嵌套的项目，然后再重新创建它们。

通常当重新加载项目时，IDE 将引发<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A>事件。 但是，对于嵌套的已删除并重新加载项目，父项目启动过程中，不在 IDE。 由于父项目不会引发解决方案的事件，并且 IDE 提供有关初始化过程的任何信息，不被引发的事件。

若要处理此过程中，父项目调用`QueryInterface`上<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents>接口。 `IVsFireSolutionEvents` 具有函数告知 IDE 引发`OnBeforeUnloadProject`事件以卸载嵌套的项目，然后引发`OnAfterLoadProject`事件来重新加载同一个项目。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- [嵌套项目](../../extensibility/internals/nesting-projects.md)