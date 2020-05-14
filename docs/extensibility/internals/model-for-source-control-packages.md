---
title: 源控制包模型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], model
ms.assetid: 6164b2d3-a622-4de8-bef3-a6de985e9ebd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 46845be1bc22a67d6703af12933945bdfcfa7f4b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707075"
---
# <a name="model-for-source-control-packages"></a>源代码管理包的模型
以下模型表示源代码管理实现的示例。 在模型中，您将看到必须实现的接口和必须调用的环境服务。 与所有服务一样，您实际上调用通过服务获取的特定接口的方法。 标识类的名称是为了更轻松地查看源代码管理是如何执行的。

 ![SCC&#95;TUP 示例](../../extensibility/internals/media/scc_tup.gif "SCC_TUP")源控制项目示例

## <a name="interfaces"></a>接口
 您可以使用下表中显示的接口列表在 Visual Studio 中实现新项目类型的源代码管理。

|接口|使用|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|在项目和编辑器保存或更改（脏）文件之前调用它们。 使用此<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>服务访问此接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|由项目调用以请求添加、删除或重命名文件或目录的权限。 项目还会调用此接口，以便在完成已批准的添加、删除或重命名操作时通知环境。 使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>服务访问它。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|由注册在项目添加、重命名或删除文件或目录时收到通知的任何实体实现。 要注册事件通知，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|被项目调用以注册源代码管理包并获取有关源代码管理状态的信息。 使用此<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>服务访问此接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|由项目实现，以响应源控制请求，以获取有关文件的信息，并获取项目文件所需的源代码管理设置。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
