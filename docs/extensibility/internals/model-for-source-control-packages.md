---
title: 源代码管理包的模型 |Microsoft Docs
description: 此模型表示源代码管理实现。 本文介绍类的名称，以便更轻松地了解源代码管理的执行方式。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 9ece2a7df1aeb2ec44f7b21075d2945a93d51838
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876684"
---
# <a name="model-for-source-control-packages"></a>源代码管理包的模型
以下模型表示源代码管理实现的示例。 在模型中，可以看到必须实现的接口和必须调用的环境服务。 与所有服务一样，实际调用通过服务获取的特定接口的方法。 标识类的名称，以便更轻松地查看源代码管理的执行方式。

 ![SCC&#95;t 示例](../../extensibility/internals/media/scc_tup.gif "SCC_TUP") 示例源代码管理项目

## <a name="interfaces"></a>界面
 可以使用下表中显示的接口列表，在 Visual Studio 中为新项目类型实现源代码管理。

|接口|用途|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|在保存或更改 (脏) 文件之前，由项目和编辑器调用。 使用服务访问此接口 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|由项目调用，请求添加、删除或重命名文件或目录的权限。 如果已批准的添加、删除或重命名操作完成，项目还将调用此接口来通知环境。 它使用服务进行访问 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|由注册为在项目添加、重命名或删除文件或目录时接收通知的任何实体实现。 若要注册事件通知，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A> 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|由项目调用以向源代码管理包注册，并获取有关源代码管理状态的信息。 使用服务访问此接口 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|由项目实现，以响应源代码管理请求，以获取有关文件的信息并获取项目文件所需的源代码管理设置。|

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
