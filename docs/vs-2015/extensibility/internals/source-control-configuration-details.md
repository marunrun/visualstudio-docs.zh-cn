---
title: 源控件配置详细信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5faa0ce575647038ac5ac7839b6dc066b7b51ce6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432065"
---
# <a name="source-control-configuration-details"></a>源代码管理配置详细信息
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

为了实现源代码管理，需要正确配置你的项目系统或编辑器执行以下操作：  
  
- 请求转换为已更改状态的权限  
  
- 请求保存文件的权限  
  
- 请求中添加、 删除或重命名项目中的文件的权限  
  
## <a name="request-permission-to-transition-to-changed-state"></a>请求转换为已更改状态的权限  
 项目或编辑器必须通过调用请求转换为已更改 （更新） 状态的权限<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>。 实现每个编辑器<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A>必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>和接收的批准才能返回之前从环境中更改文档`True`为`M:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty(System.Int32@)`。 项目是实质上是用于项目文件的编辑器中，结果是，具有相同负责实现项目文件的更改状态跟踪，文本编辑器一样为它的文件。 环境处理已更改的状态的解决方案，但必须处理任何对象，该解决方案引用，但不会存储，如项目文件或其项的已更改的状态。 一般情况下，如果你的项目或编辑器不负责管理持久性的项，然后它负责实现已更改状态跟踪。  
  
 在响应`IVsQueryEditQuerySave2::QueryEditFiles`调用，该环境可以执行以下操作：  
  
- 拒绝对更改的调用，在这种情况下的编辑器或项目必须保持不变 （清理） 状态。  
  
- 指示应重新加载文档数据。 对于项目，环境将重新加载项目的数据。 编辑器必须从通过磁盘将数据重新加载其<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>实现。 在任一情况下，重新加载数据时，可以更改项目或编辑器中的上下文。  
  
  它是一种复杂且难以实现的任务，需改进相应`IVsQueryEditQuerySave2::QueryEditFiles`到现有基本代码的调用。 因此，应在项目或编辑器的创建过程集成这些调用。  
  
## <a name="request-permission-to-save-a-file"></a>请求保存文件的权限  
 项目或编辑器在保存文件之前，必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>。 对于项目文件，这些调用会自动完成的解决方案，它知道何时将项目文件保存。 编辑器的负责进行这些调用，除非的编辑器实现`IVsPersistDocData2`使用 helper 函数<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>。 如果你的编辑器实现`IVsPersistDocData2`在这种方式，然后调用`IVsQueryEditQuerySave2::QuerySaveFile`或`IVsQueryEditQuerySave2::QuerySaveFiles`做。  
  
> [!NOTE]
> 始终提前进行这些调用 — 即，当你的编辑器是能够接收取消一次。  
  
## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>请求中添加、 删除或重命名项目中的文件的权限  
 一个项目可以添加、 重命名或删除文件或目录之前，必须调用适当`IVsTrackProjectDocuments2::OnQuery*`请求权限环境中的方法。 如果授予权限，则项目必须完成此操作，然后调用相应`IVsTrackProjectDocuments2::OnAfter*`方法以通知环境的操作已完成。 项目必须调用的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>界面，用于所有文件 （例如，特殊文件） 和不只是父文件。 文件调用是必需的但目录调用都是可选的。 如果你的项目目录的信息，则应调用相应<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>方法，但如果它没有此信息，则环境将推断目录信息。  
  
 项目不应调用的方法`IVsTrackProjectDocuments2`在项目打开或关闭。 希望将此信息在启动时的侦听器可以等待<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A>事件，并循环访问解决方案，以查找所需的信息。 关闭时，不需要此信息。 `IVsTrackProjectDocuments2` 提供从<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>。  
  
 对于每个添加、 重命名和删除操作，没有`OnQuery*`方法和一个`OnAfter*`方法。 调用`OnQuery*`方法来请求权限添加、 重命名或删除文件或目录。 调用`OnAfter*`方法后的文件或目录已添加、 重命名或删除的项目状态将反映新状态。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>   
 [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
