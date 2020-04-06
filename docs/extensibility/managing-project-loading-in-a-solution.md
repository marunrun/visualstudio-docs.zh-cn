---
title: 在解决方案中管理项目加载 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 21cd5e7e557e795db49aea7a14e8e4cc7caa0422
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702722"
---
# <a name="manage-project-loading-in-a-solution"></a>在解决方案中管理项目加载
可视化工作室解决方案可以包含大量项目。 默认 Visual Studio 行为是在打开解决方案时加载解决方案中的所有项目，并且不允许用户访问任何项目，直到这些项目都加载完。 当项目加载过程将持续两分钟以上时，将显示一个进度条，显示加载的项目数和项目总数。 用户可以在具有多个项目的解决方案中卸载项目，但此过程有一些缺点：卸载的项目不是作为重建解决方案命令的一部分构建的，并且不会显示已关闭项目的类型和成员的 IntelliSense 描述。

 开发人员可以通过创建解决方案加载管理器来缩短解决方案加载时间并管理项目加载行为。 解决方案加载管理器可以在启动后台生成之前确保加载项目，将后台加载延迟到其他后台任务完成，并执行其他项目加载管理任务。

## <a name="create-a-solution-load-manager"></a>创建解决方案负载管理器
 开发人员可以通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager>并通知 Visual Studio 解决方案负载管理器处于活动状态来创建解决方案负载管理器。

### <a name="activate-a-solution-load-manager"></a>激活解决方案负载管理器
 Visual Studio 在给定时间只允许一个解决方案加载管理器，因此当您要激活解决方案加载管理器时，您必须建议 Visual Studio。 如果稍后激活第二个解决方案负载管理器，则解决方案负载管理器将断开连接。

 您必须获得服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>并设置[__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)属性：

```csharp
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;
object objLoadMgr = this;   //the class that implements IVsSolutionManager
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);
```

 当<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A>Visual Studio 关闭时，或者当其他包通过调用 __VSPROPID4接管为活动解决方案负载管理器时，将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A>该方法[。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)属性。

#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>不同类型的解决方案负载管理器的策略
 您可以以不同的方式实施解决方案负载管理器，具体取决于它们要管理的解决方案类型。

 如果解决方案负载管理器用于管理解决方案加载，则可以将其作为 VSPackage 的一部分实现。 应通过将 VSPackage<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>上的 设置为自动加载，其值为<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid>。 然后可以在<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法中激活解决方案负载管理器。

> [!NOTE]
> 有关自动加载包的详细信息，请参阅加载[VS 包](../extensibility/loading-vspackages.md)。

 由于 Visual Studio 只识别要激活的最后一个解决方案负载管理器，因此一般解决方案负载管理器在激活自身之前应始终检测是否存在现有负载管理器。 如果调用`GetProperty()`解决方案服务[__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)返回`null`，没有活动的解决方案负载管理器。 如果未返回 null，请检查对象是否与解决方案负载管理器相同。

 如果解决方案加载管理器仅用于管理几种类型的解决方案，则 VS包可以订阅解决方案加载事件（通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>），并使用 事件处理程序<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>来激活解决方案加载管理器。

 如果解决方案负载管理器仅用于管理特定解决方案，则激活信息可以通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>解决方案前部分作为解决方案文件的一部分进行保留。

 特定解决方案负载管理器应在<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A>事件处理程序中停用自身，以免与其他解决方案负载管理器发生冲突。

 如果只需要一个解决方案加载管理器来保留全局项目加载属性（例如，在 Options 页上设置的属性），则可以在<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>事件处理程序中激活解决方案加载管理器，在解决方案属性中保留设置，然后停用解决方案加载管理器。

## <a name="handle-solution-load-events"></a>处理解决方案加载事件
 要订阅解决方案加载事件，请激活<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>解决方案加载管理器时调用。 如果实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents>，则可以响应与不同项目加载属性相关的事件。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>：在打开解决方案之前将触发此事件。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>：此事件在解决方案完全加载后触发，但在后台项目加载重新开始之前。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>： 无论是否有解决方案负载管理器，此事件是在最初完全加载解决方案后触发的。 每当解决方案完全加载时，也会在后台加载或需求加载后触发它。 同时，<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid>重新激活。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>：此事件在加载项目（或项目）之前触发。 为了确保在加载项目之前完成其他后台进程，将设置为`pfShouldDelayLoadToNextIdle` **true**。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>：当一批项目即将加载时，将触发此事件。 如果`fIsBackgroundIdleBatch`为 true，则项目将在后台加载;如果`fIsBackgroundIdleBatch`为 false，则项目将由于用户请求而同步加载，例如，如果用户在解决方案资源管理器中展开挂起的项目。 您可以处理此事件，以执行昂贵的工作，否则需要在 中<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>完成。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>：加载一批项目后，将触发此事件。

## <a name="detect-and-manage-solution-and-project-loading"></a>检测和管理解决方案和项目加载
 为了检测项目和解决方案的负载状态，使用以下值调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A>：

- [__VSPROPID4VSPROPID_IsSolutionFullyLoaded](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsSolutionFullyLoaded>) `var` ：`true`如果加载解决方案及其所有项目，则返回，否则`false`将返回 。

- [__VSPROPID4VSPROPID_IsInBackgroundIdleLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch>) `var` ：`true`如果当前在后台加载一批项目，则返回，否则返回`false`。

- [__VSPROPID4VSPROPID_IsInSyncDemandLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch>) `var` ：`true`如果一批项目当前由于用户命令或其他显式加载而同步加载，则返回，否则`false`将返回。

- [__VSPROPID2。VSPROPID_IsSolutionClosing](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2.VSPROPID_IsSolutionClosing>) `var` ：`true`如果解决方案当前正在关闭，则返回，`false`否则将返回 。

- [__VSPROPIDVSPROPID_IsSolutionOpening](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID.VSPROPID_IsSolutionOpening>) `var` ：`true`如果当前正在打开解决方案，则返回，`false`否则将返回 。

还可以通过调用以下方法之一来确保加载项目和解决方案：

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>调用此方法强制解决方案中的项目在方法返回之前加载。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>：调用此方法强制 中的项目在`guidProject`方法返回之前加载。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>：调用此方法强制项目在`guidProjectID`方法返回之前加载。
