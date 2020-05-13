---
title: 相关服务和接口（源代码管理 VS 包） |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 533f1bf4fcfbaebb25ec10908abf4a46ddacd521
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705631"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>相关服务和界面（源代码管理 VSPackage）
本节列出了 中[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]与 VSPackage 相关的所有源代码管理接口。 源代码管理 VSPackage 实现了其中一些接口，并使用其他接口来完成源代码管理任务。

## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>由 源代码管理 VS 包实现的接口，并为源代码管理 VS 包实现
 以下接口在 中介绍，[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]源代码管理 VSPackage 根据其所需的功能集实现其中的子集。 某些接口被标记为必需，并且必须由每个源代码管理 VSPackage 实现。

 对于包未实现的接口，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供默认实现。 请注意，默认实现是为未注册 VSPackage 且未控制项目的情况而设计的。 正确编写的源代码管理 VSPackage 实现所有必要的接口，而不是将其留给这些接口的默认实现。

 源代码管理 VSPackage 必须实现专用服务，该服务封装了以下部分或全部接口。

 接口包括：

- 必需：适当的实体（源代码管理 VS 包、源代码管理存根、项目）必须实现接口。

- 建议：实体应实现此接口;否则，源代码管理功能可能会受到限制。

- 可选：实体可以实现此接口，以提供更丰富的功能集。

| 接口 | 目的 | 实施者 | 实现？ |
| - | - |--------------------------|-------------|
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | 编辑人员在修改或保存文件之前调用此接口。 如果签出失败，源代码管理 VSPackage 可以签出文件或拒绝操作。 | 源代码管理 VS 包 | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | 此接口为项目提供基本源代码管理功能，例如使用源代码管理注册和取消注册项目，以及支持基本源代码管理字形。 | 源代码管理 VS 包 | 必选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> | 此<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口是从 使用 函数获得<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>，或者只需将实现`IVsHierarchy`的对象强制转换到`IVsSccProject2`。 它用于在项目中使文件处于源代码管理之下，或通知项目当前源代码管理状态或位置。 | Project | 必选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> | 集成模块使用此接口设置当前活动 VSPackage。 | 源代码管理 VS 包 | 必选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> | 此接口基于订阅模型。 任何 VSPackage 都可以发出信号，表明它要接收文档事件，并且 shell 会就即将发生的事件提供建议。 它由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实现和处理，后者又将实现的事件`IVsTrackProjectDocumentsEvents2`传递给 VSPackage。 | 源代码管理存根 | 必选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | 此接口提供批处理、同步读/写操作和高级`OnQueryAddFiles`方法。 | 源代码管理存根 | 必选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> | 当向项目添加新文件或从项目重命名或删除文件和文件夹时，**解决方案资源管理器**和项目将调用此接口。 源代码管理 VSPackage 可以签出项目文件或取消操作。 | 源代码管理 VS 包 | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3> | **解决方案资源管理器**和项目调用此接口以响应对 IVtrackProjectDocuments3 接口方法的调用。 源代码管理 VSPackage 可以跟踪批处理操作、同步读/写操作，以及使用更高级`OnQueryAddFiles`的方法。 | 源代码管理 VS 包 | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation> | 此接口为 Web 项目提供登记管理支持。 | 源代码管理 VS 包 | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip> | 此接口用于检索项目中源控制文件的 ToolTips。 | 源代码管理 VS 包 | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl> | 此接口提供命名空间扩展支持。 | 源代码管理 VS 包 | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution> | VSPackage 使用此接口将命名空间扩展集成到 **"新建****"、"打开"** 或 **"保存"** 对话框中。 因此，可以在创建时自动将项目添加到源代码管理中，或在保存操作生效时将其添加到源代码管理。 | 源代码管理 VS 包 | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> | VSPackage 使用此接口将其他字形定义为**解决方案资源管理器**中节点的源代码管理字形。 | 源代码管理 VS 包 | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl> | Web 项目的 **"添加**"对话框使用此界面。 它提供了用于浏览源代码管理位置的方法，以及打开以前添加到该位置的源代码管理存储库中的 Web 项目的方法。 | 源代码管理 VS 包 | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> | 此接口支持从源代码管理加载项目的异步（后台）加载。 | 源代码管理 VS 包 | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents> | 此接口允许项目监视由<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc>启动的异步加载的进度。 | Project | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | 此接口允许 IDE 查询活动源控件 VSPackage。 IDE 查询源代码管理设置的值，即使未注册活动源代码管理 VSPackage，这些设置也具有意义。 此接口由 实现[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和处理。 | 源代码管理存根 | 必选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> | 此接口用于注册源代码管理 VSPackage。 | 源代码管理存根 | 必选 |
| <xref:EnvDTE.SourceControl> | 此接口用于自动化。 因此，它只公开可以在不显示任何 UI 的情况下执行的功能。 | 源代码管理 VS 包 | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> | 此接口用于将源代码管理设置保存在解决方案 （.sln） 文件中。 这些设置包括源代码管理位置和源代码管理状态标志。 | 源代码管理 VS 包 | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> | 此接口用于将源代码管理设置保存在解决方案选项 （.suo） 文件中。 这可能包括特定于用户的源代码管理设置，如当前用户的登记位置。 | 源代码管理 VS 包 | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> | 此接口用于监视事件，以便执行操作，例如在关闭解决方案之前签入项目文件，或在打开项目时从源代码管理获取新文件。 | 源代码管理 VS 包 | 建议 |

## <a name="see-also"></a>请参阅
- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
