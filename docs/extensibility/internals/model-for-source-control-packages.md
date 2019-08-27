---
title: 源代码管理包模型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], model
ms.assetid: 6164b2d3-a622-4de8-bef3-a6de985e9ebd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65f212496d152236579e63ba037fe351a4dd3370
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349225"
---
# <a name="model-for-source-control-packages"></a>源代码管理包的模型
以下模型表示源控件实现的示例。 在模型中，您可以看到必须实现的接口和必须调用环境服务。 类似于所有服务，实际调用通过该服务获取特定接口的方法。 类的名称进行标识，以便更轻松地查看如何执行源代码管理。

 ![SCC&#95;/{TUP 示例](../../extensibility/internals/media/scc_tup.gif "SCC_TUP")示例源代码管理项目

## <a name="interfaces"></a>接口
 您可以在 Visual Studio 中使用的以下表中所示的接口列表中将新项目类型实现源代码管理。

|接口|使用|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|由项目和编辑器保存它们或更改 （更新） 文件之前调用。 使用访问此接口<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>服务。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|调用由请求权限以添加、 删除或重命名文件或目录的项目。 若要通知的环境时已批准的添加、 删除或重命名操作已完成的项目还会调用此接口。 使用访问<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>服务。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|由注册项目添加、 重命名或删除文件或目录时要通知的任何实体实现。 若要注册事件通知，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|调用项目源代码管理包中注册并获取源代码管理状态的信息。 使用访问此接口<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>服务。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|实现对文件的信息的源控件请求做出响应并获取项目文件所需的控制设置的源项目。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)