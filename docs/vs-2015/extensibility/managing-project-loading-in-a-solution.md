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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63426450"
---
# <a name="managing-project-loading-in-a-solution"></a>管理解决方案中的项目加载
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 解决方案可以包含大量的项目。 默认 Visual Studio 行为是打开解决方案时，次加载解决方案中的所有项目并不允许用户访问任何项目，直到所有这些已完成加载为止。 当项目加载过程将持续时间超过两分钟时，被显示一个进度栏显示加载的项目数量以及项目总数。 用户可以在具有多个项目的解决方案中使用时，卸载项目，但此过程也有一些缺点： 已卸载的项目不是作为重新生成解决方案命令，并关闭 IntelliSense 类型的说明和的成员项目不会显示。  
  
 开发人员可以减少解决方案加载时间和管理项目管理器中创建解决方案加载的加载行为。 解决方案负载管理器可以设置不同的项目加载特定项目或项目类型的优先级，请确保在开始后台生成之前加载了项目、 延迟后台加载其他后台任务完成之前, 并执行其他项目负载管理任务。  
  
## <a name="project-loading-priorities"></a>项目加载优先级  
 Visual Studio 定义四个不同的项目加载优先级：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority> （默认值）： 打开解决方案时，以异步方式加载项目。 如果已打开该解决方案后，已卸载的项目上设置此优先级，则将在下一个空闲点加载该项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>： 当打开解决方案时，将项目加载在后台，这样就允许用户访问的项目，因为它们是加载而无需等待，直到已加载所有项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>： 进行访问时加载项目。 一个项目或解决方案打开后，因为它是在打开的文档列表中 （保留在解决方案的用户选项文件），打开文件属于项目时，在用户展开解决方案资源管理器中的项目节点时访问另一个项目它是正在加载具有项目的依赖关系。 此类型的项目不自动加载之前启动的生成过程;在解决方案加载管理器负责确保加载所需的所有项目。 此外应在整个解决方案文件中开始查找/替换之前加载这些项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>： 项目将不能加载，除非用户明确请求它。 当项目显式卸载时，这是这种情况。  
  
## <a name="creating-a-solution-load-manager"></a>管理器中创建解决方案加载  
 开发人员可以创建解决方案加载管理器通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager>并告知 Visual Studio 解决方案负载管理器处于活动状态。  
  
#### <a name="activating-a-solution-load-manager"></a>激活解决方案负载管理器  
 Visual Studio，只有一个解决方案负载管理器在给定时间，因此当你想要激活解决方案加载时，你必须告知 Visual Studio 管理器。 如果第二个解决方案负载管理器已激活更高版本上，将断开解决方案负载管理器。  
  
 必须获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>服务并设置<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>属性：  
  
```csharp  
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;  
object objLoadMgr = this;   //the class that implements IVsSolutionManager  
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);  
```  
  
#### <a name="implementing-ivssolutionloadmanager"></a>实现 IVsSolutionLoadManager  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnBeforeOpenProject%2A>打开解决方案的过程中调用方法。 若要实现此方法，您可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManagerSupport>服务，将设置你想要管理的项目的类型的负载优先级。 例如，下面的代码设置 C# 项目类型在后台加载：  
  
```csharp  
Guid guidCSProjectType = new Guid("{FAE04EC0-301F-11d3-BF4B-00C04F79EFBC}");  
pSLMgrSupport.SetProjectLoadPriority(guidProjectID, (uint)_VSProjectLoadPriority.PLP_BackgroundLoad);  
```  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A>正在关闭 Visual Studio 或不同的包会充当活动解决方案负载管理器通过调用时调用方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A>与<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>属性。  
  
#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>为不同类型的解决方案负载管理器策略  
 您可以在不同的方式，具体取决于它们专门用于管理的解决方案的类型的实现解决方案负载管理器。  
  
 如果解决方案负载管理器要管理的一般情况下加载的解决方案，它可实现 VSPackage 的一部分。 通过添加，应将包设置为自动加载<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>上的值为 VSPackage <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid>。 然后可以在激活解决方案负载管理器<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法。  
  
> [!NOTE]
> 有关自动加载包的详细信息，请参阅[加载 Vspackage](../extensibility/loading-vspackages.md)。  
  
 因为 Visual Studio 能够识别仅在最后一个解决方案负载管理器来激活，通用的解决方案负载经理应该始终首先检测是否存在现有的负载管理器在激活本身之前。 如果解决方案服务上调用 GetProperty()<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>返回`null`，没有活动解决方案负载管理器。 如果它不返回 null，则检查对象是否与解决方案负载管理器相同。  
  
 如果解决方案负载管理器旨在管理仅几种类型的解决方案，VSPackage 可以订阅解决方案负载事件 (通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>)，并使用的事件处理程序<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>激活解决方案负载管理器。  
  
 如果解决方案负载管理器旨在管理仅特定解决方案，可作为解决方案文件的一部分保留激活信息。 若要执行此操作，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>预解决方案部分。  
  
 特定解决方案负载经理应停用本身中<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A>事件处理程序，为了不与其他解决方案负载管理器发生冲突。  
  
 如果仅要持久保存全局项目负载优先顺序 （例如，在选项页上设置的属性），可以激活中的解决方案负载管理器需要解决方案负载管理器<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents2.OnAfterOpenProject%2A>事件处理程序，然后在解决方案属性设置保留停用解决方案负载管理器。  
  
## <a name="handling-solution-load-events"></a>处理解决方案负载事件  
 若要订阅的解决方案加载事件，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>激活解决方案负载管理器。 如果你实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents>，可以响应的不同项目加载优先级与相关的事件。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>：这被触发之前打开解决方案。 可用于更改项目加载解决方案中项目的优先级。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>：这后的解决方案是完全加载，但后台加载的项目开始之前再次激发。 例如，用户可能已访问其负载优先级是 LoadIfNeeded，一个项目或解决方案负载管理器可能已更改项目负载优先级，为 BackgroundLoad，将启动该项目的背景加载。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>：这后激发一开始完全加载解决方案时，不存在解决方案负载管理器。 后台负载或需加载时解决方案变得完全加载后，它也会激发。 同时，在<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid>重新激活。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>：这会触发之前加载的项目 （或项目）。 若要确保加载项目之前完成其他后台进程，设置`pfShouldDelayLoadToNextIdle`到**true**。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>：这一批的项目是加载时触发。 如果`fIsBackgroundIdleBatch`为 true 的项目是加载在后台中; 如果`fIsBackgroundIdleBatch`为 false 的项目是要加载同步由于用户请求，例如在用户如果展开解决方案资源管理器中的挂起的项目。 您可以实现此执行成本高昂的工作，否则需要完成<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>：这被触发加载项目一批之后。  
  
## <a name="detecting-and-managing-solution-and-project-loading"></a>检测和管理解决方案和项目加载  
 若要检测的项目和解决方案加载状态，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A>使用以下值：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>:`var`将返回`true`解决方案和所有项目已加载，否则如果`false`。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>:`var`将返回`true`如果一批项目当前正在加载在后台，否则`false`。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>:`var`将返回`true`如果一批项目当前正在加载以同步方式由于用户命令或其他显式负载，否则`false`。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>:`var`将返回`true`解决方案当前正在关闭，否则如果`false`。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>:`var`将返回`true`当前正在打开解决方案，否则如果`false`。  
  
  此外可以通过调用以下方法之一来确保项目和解决方案加载 （无论项目负载优先顺序是什么）：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>： 调用此方法会强制加载完毕，该方法将返回解决方案中的项目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>： 调用此方法会强制在项目`guidProject`加载完毕，该方法返回。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>： 调用此方法会强制中的项目`guidProjectID`加载完毕，该方法返回。  
  
> [!NOTE]
> . 默认情况下仅有需求的项目加载和后台负载优先级已加载，但如果<xref:Microsoft.VisualStudio.Shell.Interop.__VSBSLFLAGS>标志中传递给方法，所有项目将都加载的标记来显式加载除外。
