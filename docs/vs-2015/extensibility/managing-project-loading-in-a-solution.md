---
title: 管理解决方案中的项目加载 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a6598e2f1a178845b3ad2017716576439185379e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840387"
---
# <a name="managing-project-loading-in-a-solution"></a>管理解决方案中的项目加载
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 解决方案可以包含大量项目。 默认的 Visual Studio 行为是在解决方案打开时加载解决方案中的所有项目，而不允许用户访问任何项目，直到所有项目都完成加载。 当项目加载过程的持续时间超过两分钟时，将显示一个进度栏，其中显示了已加载的项目数和项目总数。 在包含多个项目的解决方案中工作时，用户可以卸载项目，但此过程存在一些缺点：卸载的项目不是作为 "重新生成解决方案" 命令的一部分生成的，并且不会显示类型和关闭项目的成员的 IntelliSense 说明。  
  
 开发人员可以通过创建解决方案负载管理器来减少解决方案加载时间并管理项目加载行为。 解决方案负载管理器可以为特定项目或项目类型设置不同的项目加载优先级，请确保在启动后台生成之前加载项目，延迟后台加载，直到完成其他后台任务，以及执行其他项目负载管理任务。  
  
## <a name="project-loading-priorities"></a>项目加载优先级  
 Visual Studio 定义四个不同的项目加载优先级：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority> (默认) ：打开解决方案时，会以异步方式加载项目。 如果在解决方案已打开后在已卸载的项目上设置此优先级，则会在下一个空闲点加载该项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>：打开解决方案时，将在后台加载项目，使用户可以在加载项目时访问项目，而无需等待加载所有项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>：在访问项目时将其加载。 当解决方案打开时，如果项目是在打开的文档列表中 (保存在打开的文档列表中，而该项目是在解决方案的用户选项文件) 中保存的，或者如果正在加载的另一个项目依赖于项目，则当用户展开解决方案资源管理器中的项目节点时，将访问项目。 此类型的项目在启动生成过程之前不会自动加载;解决方案负载管理器负责确保加载所有必要的项目。 在整个解决方案中的文件中启动查找/替换之前，还应加载这些项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>：除非用户显式请求项目，否则不会加载项目。 这是显式卸载项目的情况。  
  
## <a name="creating-a-solution-load-manager"></a>创建解决方案负载管理器  
 开发人员可以通过实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager> 并通知 Visual Studio 解决方案负载管理器处于活动状态来创建解决方案负载管理器。  
  
#### <a name="activating-a-solution-load-manager"></a>激活解决方案负载管理器  
 Visual Studio 在给定时间只允许使用一个解决方案负载管理器，因此当你想要激活解决方案负载管理器时，你必须建议使用 Visual Studio。 如果稍后激活第二个解决方案加载管理器，则解决方案加载管理器将断开连接。  
  
 必须获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> 服务并设置 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> 属性：  
  
```csharp  
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;  
object objLoadMgr = this;   //the class that implements IVsSolutionManager  
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);  
```  
  
#### <a name="implementing-ivssolutionloadmanager"></a>实现 IVsSolutionLoadManager  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnBeforeOpenProject%2A>方法是在打开解决方案的过程中调用的。 若要实现此方法，请使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManagerSupport> 服务为你要管理的项目类型设置加载优先级。 例如，以下代码将 c # 项目类型设置为在后台加载：  
  
```csharp  
Guid guidCSProjectType = new Guid("{FAE04EC0-301F-11d3-BF4B-00C04F79EFBC}");  
pSLMgrSupport.SetProjectLoadPriority(guidProjectID, (uint)_VSProjectLoadPriority.PLP_BackgroundLoad);  
```  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A>当关闭 Visual Studio 或使用属性调用其他包作为活动解决方案加载管理器时，将调用方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> 。  
  
#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>不同种类的解决方案负载管理器的策略  
 可以通过不同的方式实现解决方案负载管理器，具体取决于要管理的解决方案的类型。  
  
 如果解决方案负载管理器打算一般管理解决方案加载，则可以将其作为 VSPackage 的一部分实现。 应将包设置为 autoload，方法是 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 在 VSPackage 上添加值为的 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid> 。 然后，可以在方法中激活解决方案负载管理器 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 。  
  
> [!NOTE]
> 有关自动加载包的详细信息，请参阅 [加载 vspackage](../extensibility/loading-vspackages.md)。  
  
 由于 Visual Studio 仅识别要激活的最后一个解决方案加载管理器，一般的解决方案负载管理器应始终检测是否存在现有的负载管理器，然后才能激活自身。 如果在返回的解决方案服务中调用 GetProperty ( # <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> A1 `null` ，则没有活动的解决方案负载管理器。 如果它不返回 null，请检查对象是否与您的解决方案负载管理器相同。  
  
 如果解决方案负载管理器旨在仅管理几种类型的解决方案，则 VSPackage 可以通过调用)  (订阅解决方案加载事件， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> 并使用的事件处理程序 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A> 来激活解决方案加载管理器。  
  
 如果解决方案负载管理器仅用于管理特定解决方案，则可以将激活信息作为解决方案文件的一部分保存。 为此，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> "预先解决方案" 部分。  
  
 特定解决方案负载管理器应在事件处理程序中停用自身 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A> ，以使其不会与其他解决方案负载管理器冲突。  
  
 如果你只需要解决方案负载管理器来持久保存全局项目负载优先级 (例如，在 "选项" 页) 上设置的属性，则可以在事件处理程序中激活解决方案负载管理器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents2.OnAfterOpenProject%2A> ，在解决方案属性中保留设置，然后停用解决方案加载管理器。  
  
## <a name="handling-solution-load-events"></a>处理解决方案加载事件  
 若要订阅解决方案加载事件，请 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> 在激活解决方案负载管理器时调用。 如果实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents> ，则可以对与不同项目加载优先级相关的事件做出响应。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>：在打开解决方案之前触发此操作。 您可以使用它更改解决方案中项目的项目加载优先级。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>：此操作在解决方案完全加载后，但在后台项目加载再次开始之前激发。 例如，用户可能访问了加载优先级为 LoadIfNeeded 的项目，或者解决方案负载管理器可能已将项目加载优先级更改为 BackgroundLoad，这将启动该项目的后台加载。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>：最初完全加载解决方案后，无论是否存在解决方案负载管理器，都将激发此情况。 当解决方案完全加载后，还会在后台加载或要求加载后触发。 同时， <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid> 重新激活。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>：在 (或项目的加载) 加载之前触发此操作。 若要确保在加载项目之前完成其他后台进程，请将设置 `pfShouldDelayLoadToNextIdle` 为 **true**。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>：当要加载一批项目时，将触发此操作。 如果 `fIsBackgroundIdleBatch` 为 true，则将在后台加载项目; 如果 `fIsBackgroundIdleBatch` 为 false，则将以用户请求的形式同步加载项目，例如，用户在解决方案资源管理器展开挂起项目。 您可以实现此目的来完成需要在中完成的成本高昂的工作 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> 。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>：加载一批项目后，将触发此情况。  
  
## <a name="detecting-and-managing-solution-and-project-loading"></a>检测和管理解决方案和项目加载  
 若要检测项目和解决方案的加载状态，请调用， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A> 并提供以下值：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>： `var` `true` 如果已加载解决方案及其所有项目，则返回; 否则返回 `false` 。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>： `var` `true` 如果当前正在后台加载一批项目，则返回; 否则返回 `false` 。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>： `var` `true` 如果由于用户命令或其他显式负载而当前正在同步加载一批项目，则返回; 否则返回 `false` 。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>： `var` `true` 如果当前正在关闭解决方案，则返回; 否则返回 `false` 。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>： `var` `true` 如果当前正在打开解决方案，则返回; 否则返回 `false` 。  
  
  你还可以通过调用以下方法之一，确保 (加载项目和解决方案，而不考虑项目负载优先级) ：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>：调用此方法会强制解决方案中的项目在方法返回之前加载。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>：调用此方法会强制在 `guidProject` 方法返回之前加载中的项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>：调用此方法会强制在 `guidProjectID` 方法返回之前加载中的项目。  
  
> [!NOTE]
> . 默认情况下，仅加载具有 "要求加载" 和 "后台加载" 优先级的项目，但如果将 <xref:Microsoft.VisualStudio.Shell.Interop.__VSBSLFLAGS> 标志传递给方法，则将加载所有项目（标记为显式加载的项目除外）。
