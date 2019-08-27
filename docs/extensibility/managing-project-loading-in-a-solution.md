---
title: 管理解决方案中的项目加载 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a80430c4a5dcf5526445275b89fa2da7f02f5529
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340581"
---
# <a name="manage-project-loading-in-a-solution"></a>管理解决方案中的项目加载
Visual Studio 解决方案可以包含大量的项目。 默认 Visual Studio 行为是打开解决方案时，次加载解决方案中的所有项目并不允许用户访问任何项目，直到所有这些已完成加载为止。 当项目加载过程将持续时间超过两分钟时，被显示一个进度栏显示加载的项目数量以及项目总数。 用户可以在具有多个项目的解决方案中使用时，卸载项目，但此过程也有一些缺点： 已卸载的项目不是作为重新生成解决方案命令，并关闭 IntelliSense 类型的说明和的成员项目不会显示。

 开发人员可以减少解决方案加载时间和管理项目管理器中创建解决方案加载的加载行为。 解决方案负载管理器可以确保在开始后台生成之前加载了项目、 后台加载其他后台任务完成之前, 的延迟和执行其他项目负载管理任务。

## <a name="create-a-solution-load-manager"></a>管理器中创建解决方案加载
 开发人员可以创建解决方案加载管理器通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager>并告知 Visual Studio 解决方案负载管理器处于活动状态。

### <a name="activate-a-solution-load-manager"></a>激活解决方案负载管理器
 Visual Studio，只有一个解决方案负载管理器在给定时间，因此当你想要激活解决方案加载时，你必须告知 Visual Studio 管理器。 如果第二个解决方案负载管理器已激活更高版本上，将断开解决方案负载管理器。

 必须获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>服务并设置[__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)属性：

```csharp
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;
object objLoadMgr = this;   //the class that implements IVsSolutionManager
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);
```

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A>正在关闭 Visual Studio 或不同的包会充当活动解决方案负载管理器通过调用时调用方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A>与[__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)属性。

#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>为不同类型的解决方案负载管理器策略
 您可以在不同的方式，具体取决于它们专门用于管理的解决方案的类型的实现解决方案负载管理器。

 如果解决方案负载管理器要管理的一般情况下加载的解决方案，它可实现 VSPackage 的一部分。 通过添加，应将包设置为自动加载<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>上的值为 VSPackage <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid>。 然后可以在激活解决方案负载管理器<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法。

> [!NOTE]
> 有关自动加载包的详细信息，请参阅[加载 Vspackage](../extensibility/loading-vspackages.md)。

 因为 Visual Studio 能够识别仅在最后一个解决方案负载管理器来激活，通用的解决方案负载经理应该始终首先检测是否存在现有的负载管理器在激活本身之前。 如果调用`GetProperty()`上的解决方案服务[__VSPROPID4。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)返回`null`，没有活动解决方案负载管理器。 如果它不返回 null，则检查对象是否与解决方案负载管理器相同。

 如果解决方案负载管理器旨在管理仅几种类型的解决方案，VSPackage 可以订阅解决方案负载事件 (通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>)，并使用的事件处理程序<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>激活解决方案负载管理器。

 如果解决方案负载管理器旨在管理仅特定解决方案，可以通过调用保持为解决方案文件的一部分的激活信息<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>预解决方案部分。

 特定解决方案负载经理应停用本身中<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A>事件处理程序，为了不与其他解决方案负载管理器发生冲突。

 如果仅要持久保存全局项目负载属性 （例如，在选项页上设置的属性），可以激活中的解决方案负载管理器需要解决方案负载管理器<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>事件处理程序，然后在解决方案属性设置保留停用解决方案负载管理器。

## <a name="handle-solution-load-events"></a>处理解决方案负载事件
 若要订阅的解决方案加载事件，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>激活解决方案负载管理器。 如果你实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents>，可以为到不同的项目加载属性相关的事件的响应。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>：打开一个解决方案之前，触发此事件。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>：之后的解决方案是完全加载，但后台加载的项目开始之前再次激发此事件。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>：此事件后激发一开始完全加载解决方案时，不存在解决方案负载管理器。 后台负载或需加载时解决方案变得完全加载后，它也会激发。 同时，在<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid>重新激活。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>：在加载项目 （或项目） 之前触发此事件。 若要确保加载项目之前完成其他后台进程，设置`pfShouldDelayLoadToNextIdle`到**true**。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>：加载项目一批时，触发此事件。 如果`fIsBackgroundIdleBatch`为 true 的项目是加载在后台中; 如果`fIsBackgroundIdleBatch`为 false 的项目是要加载同步由于用户请求，例如在用户如果展开解决方案资源管理器中的挂起的项目。 可以处理此事件来执行成本高昂的工作，否则需要完成<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>：加载项目一批之后激发此事件。

## <a name="detect-and-manage-solution-and-project-loading"></a>检测和管理解决方案和项目加载
 若要检测的项目和解决方案加载状态，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A>使用以下值：

- [__VSPROPID4。VSPROPID_IsSolutionFullyLoaded](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsSolutionFullyLoaded>):`var`返回`true`解决方案，其所有项目均已加载，否则如果`false`。

- [__VSPROPID4。VSPROPID_IsInBackgroundIdleLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch>):`var`返回`true`如果一批项目当前正在加载在后台，否则`false`。

- [__VSPROPID4。VSPROPID_IsInSyncDemandLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch>):`var`返回`true`如果一批项目当前正在加载同步由于用户命令或其他显式负载，否则`false`。

- [__VSPROPID2。VSPROPID_IsSolutionClosing](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2.VSPROPID_IsSolutionClosing>):`var`返回`true`解决方案当前正在关闭，否则如果`false`。

- [__VSPROPID。VSPROPID_IsSolutionOpening](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID.VSPROPID_IsSolutionOpening>):`var`返回`true`如果当前正在打开解决方案，否则`false`。

您还可以确保项目和解决方案加载通过调用以下方法之一：

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>： 调用此方法会强制加载完毕，该方法将返回解决方案中的项目。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>： 调用此方法会强制在项目`guidProject`加载完毕，该方法返回。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>： 调用此方法会强制中的项目`guidProjectID`加载完毕，该方法返回。
