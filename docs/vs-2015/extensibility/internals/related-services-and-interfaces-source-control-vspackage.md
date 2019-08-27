---
title: 相关的服务和界面 (源代码管理 VSPackage) |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157396"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>相关服务和界面（源代码管理 VSPackage）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本部分列出了所有的源控件中的 VSPackage 相关接口[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]。 源代码管理 VSPackage 实现这些接口的一些，并使用其他人来完成源代码管理任务。  
  
## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>接口和源代码管理 Vspackage 的实现  
 中介绍了以下接口[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]，和源代码管理 VSPackage 实现其子集的具体取决于其所需的功能集。 一些接口来标记作为所需，必须由每个源代码管理 VSPackage 实现。  
  
 包未实现时，这些接口[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]提供默认实现。 请注意，默认实现设计的情况下不注册任何 VSPackage 和不控制任何项目时。 正确编写的源代码管理 VSPackage 实现所有必要的接口，而不是将它保留为这些接口的默认实现。  
  
 源代码管理 VSPackage 必须实现封装的部分或所有以下接口的专用服务。  
  
 接口是：  
  
- 必需：相应的实体 （源代码管理 VSPackage，源存根 （stub） 项目） 必须实现接口。  
  
- 建议：实体应实现此接口;否则，源代码管理功能，可能会受到限制。  
  
- 可选： 实体可以实现此接口可提供更丰富的功能集。  
  
|接口|用途|由实现|实现？|  
|---------------|-------------|--------------------|----------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|编辑器调用此接口，然后再修改或保存文件。 源代码管理 VSPackage 可以签出该文件或拒绝该操作，如果签出失败。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|此接口提供基本源代码管理功能，对于项目，如注册和取消注册与源代码管理项目和基本源控件中绘制标志符号提供支持。|源代码管理 VSPackage|必填|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|此接口从获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>使用<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>函数，或只需强制转换对象实现`IVsHierarchy`到`IVsSccProject2`。 它所获取的项目中的源控件下的文件或通知的当前源代码管理状态或位置的项目。|项目|必填|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>|集成模块使用此接口来设置当前活动的 VSPackage。|源代码管理 VSPackage|必填|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|此接口基于订阅模型。 任何 VSPackage 可以指示它希望接收文档事件需要注意 shell 上将要发生的事件。 实现并由[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，这反过来将实现的事件传递`IVsTrackProjectDocumentsEvents2`到 VSPackage。|源存根 （stub)|必填|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3>|此接口提供了批处理、 同步的读/写操作和一种高级`OnQueryAddFiles`方法。|源存根 （stub)|必填|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|**解决方案资源管理器**和新文件添加到项目，或重命名或从项目中删除文件和文件夹时，项目将调用此接口。 源代码管理 VSPackage 可以签出项目文件或取消操作。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3>|**解决方案资源管理器**和项目调用以响应对 IVstrackProjectDocuments3 接口的方法的调用此接口。 源代码管理 VSPackage 可以跟踪批处理的操作，同步读/写操作，并使用更高级`OnQueryAddFiles`方法。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation>|此接口提供登记管理 Web 项目的支持。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip>|此接口用于检索项目的源代码管理文件的工具提示。|源代码管理 VSPackage|Optional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl>|此接口提供的命名空间扩展支持。|源代码管理 VSPackage|Optional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution>|VSPackage 使用此接口将集成到一个命名空间扩展**新建**，**打开**，或**保存**对话框。 因此，项目可以自动添加到源代码管理在创建时，或添加到源代码管理时保存操作已生效。|源代码管理 VSPackage|Optional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>|VSPackage 使用此接口定义为源控件中的节点的标志符号的其他标志符号**解决方案资源管理器**。|源代码管理 VSPackage|Optional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl>|**添加**Web 项目的对话框中使用此接口。 它提供用于浏览源代码管理位置以及用于打开以前在该位置的源控件存储库中添加一个 Web 项目的方法。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc>|此接口提供异步 （后台） 加载从源代码管理项目的支持。|源代码管理 VSPackage|Optional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents>|此接口允许项目以查看由启动异步加载进度<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc>。|项目|Optional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions>|此接口允许在 IDE 来查询活动的源代码管理 VSPackage。 在 IDE 中查询具有意义，即使没有 VSPackage 注册活动的源控件的源代码管理设置的值。 此接口实现，由处理[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。|源存根 （stub)|必填|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>|在注册源代码管理 VSPackage 中使用此接口。|源存根 （stub)|必填|  
|<xref:EnvDTE.SourceControl>|在自动化中使用此接口。 在这种情况下，它公开可以但不显示任何 UI 执行的函数。|源代码管理 VSPackage|Optional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>|此接口用于将源控件设置保存在解决方案 (.sln) 文件。 设置包括源代码管理位置和源控件状态标志。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>|此接口用于解决方案选项 (.suo) 文件中保存源代码管理设置。 这可能包括特定于用户的源代码管理设置，例如当前用户的登记位置。|源代码管理 VSPackage|建议|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>|此接口用于监视事件以执行操作，如签入之前关闭解决方案，或从源代码管理获取新文件，在打开项目的项目文件。|源代码管理 VSPackage|建议|  
  
## <a name="see-also"></a>请参阅  
 [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
