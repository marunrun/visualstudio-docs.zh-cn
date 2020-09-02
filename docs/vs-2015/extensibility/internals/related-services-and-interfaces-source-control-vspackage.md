---
title: 相关服务和接口 (源代码管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0c5b040a8c5d0cbe2daff07f279cfd6a78cbd2b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157396"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>相关服务和界面（源代码管理 VSPackage）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本部分列出了中与源代码管理 VSPackage 相关的所有接口 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 。 源代码管理 VSPackage 实现其中一些接口，并使用其他接口来完成源代码管理任务。  
  
## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>为源代码管理实现和实现的接口 Vspackage  
 中介绍了以下接口 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] ，源代码管理 VSPackage 根据所需的功能集实现这些接口的子集。 某些接口标记为必需，必须由每个源代码管理 VSPackage 实现。  
  
 对于包不实现的接口， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 提供默认实现。 请注意，默认实现适用于未注册 VSPackage 并且未控制任何项目的情况。 正确编写的源代码管理 VSPackage 实现所有必需的接口，而不是将其保留到这些接口的默认实现。  
  
 源代码管理 VSPackage 必须实现一个专用服务，该服务封装以下部分或所有接口。  
  
 接口包括：  
  
- 必需：相应的实体 (源控件 VSPackage、源代码管理存根、项目) 必须实现接口。  
  
- 建议：实体应实现此接口;否则，源代码管理功能可能会受到限制。  
  
- 可选：实体可以实现此接口以提供更丰富的功能集。  
  
|接口|用途|实现者|实施?|  
|---------------|-------------|--------------------|----------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|编辑器在修改或保存文件之前调用此接口。 如果签出失败，则源代码管理 VSPackage 可以签出文件或拒绝操作。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|此接口提供了项目的基本源代码管理功能，例如，通过源代码管理注册和注销项目，并提供对基本源控件标志符号的支持。|源代码管理 VSPackage|必需|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|此接口是 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 使用函数获取的 <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> ，或者只是将实现的对象强制转换 `IVsHierarchy` 为 `IVsSccProject2` 。 它用于在项目中获取源代码管理下的文件或通知项目当前源代码管理状态或位置。|Project|必需|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>|集成模块使用此接口设置当前活动的 VSPackage。|源代码管理 VSPackage|必需|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|此接口基于订阅模型。 任何 VSPackage 都可以发出信号，指示它希望接收文档事件，并在即将发生的事件上通知 shell。 它由实现并处理 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，后者又将实现的事件传递 `IVsTrackProjectDocumentsEvents2` 给 VSPackage。|源代码管理存根|必需|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3>|此接口提供批处理、同步读/写操作和高级 `OnQueryAddFiles` 方法。|源代码管理存根|必需|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|当将新文件添加到项目中时，或在项目中重命名或删除文件和文件夹时，**解决方案资源管理器**和项目将调用此接口。 源代码管理 VSPackage 可以签出项目文件或取消该操作。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3>|**解决方案资源管理器** 和项目调用此接口，以响应对 IVstrackProjectDocuments3 接口的方法所做的调用。 源代码管理 VSPackage 可以跟踪批处理操作、同步读/写操作以及使用更高级的 `OnQueryAddFiles` 方法。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation>|此接口提供对 Web 项目的登记管理支持。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip>|此接口用于检索项目中受源代码管理的文件的工具提示。|源代码管理 VSPackage|可选|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl>|此接口提供命名空间扩展支持。|源代码管理 VSPackage|可选|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution>|VSPackage 使用此接口将命名空间扩展集成到 " **新建**"、" **打开**" 或 " **保存** " 对话框中。 因此，项目可以在创建时自动添加到源代码管理，或在保存操作生效时添加到源代码管理。|源代码管理 VSPackage|可选|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>|VSPackage 使用此接口将其他标志符号定义为 **解决方案资源管理器**中的节点的源代码管理标志符号。|源代码管理 VSPackage|可选|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl>|Web 项目的 " **添加** " 对话框使用此接口。 它提供用于浏览源代码管理位置和打开之前在该位置添加到源代码管理存储库中的 Web 项目的方法。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc>|此接口提供对异步 (后台) 从源代码管理加载项目的支持。|源代码管理 VSPackage|可选|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents>|此接口允许项目监视由启动的异步加载的进度 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> 。|Project|可选|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions>|此接口允许 IDE 查询活动源代码管理 VSPackage。 即使没有已注册的活动源代码管理 VSPackage，IDE 也会查询具有意义的源代码管理设置的值。 此接口由实现和处理 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。|源代码管理存根|必需|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>|此接口用于注册源代码管理 VSPackage。|源代码管理存根|必需|  
|<xref:EnvDTE.SourceControl>|此接口在自动化中使用。 因此，它只公开可以在不显示任何用户界面的情况下执行的函数。|源代码管理 VSPackage|可选|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>|此接口用于将源代码管理设置保存到解决方案 ( .sln) 文件中。 这些设置包括源代码管理位置和源代码管理状态标志。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>|此接口用于将源代码管理设置保存到解决方案选项 ( .suo) 文件中。 这可能包括用户特定的源代码管理设置，如当前用户的登记位置。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>|此接口用于监视事件，以便执行操作（如在关闭解决方案之前签入项目文件，或在打开项目时从源代码管理获取新文件）。|源代码管理 VSPackage|建议|  
  
## <a name="see-also"></a>另请参阅  
 [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
