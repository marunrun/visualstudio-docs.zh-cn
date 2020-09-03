---
title: 使用旧 API 访问 theText 视图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text view
ms.assetid: 8f751f72-c972-4be3-84ee-19c281e02e25
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f9396e4523e38e7313efb5668c4680f551558ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184958"
---
# <a name="accessing-thetext-view-by-using-the-legacy-api"></a>使用旧版 API 访问文本视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本视图是文本缓冲区中存储的文本的表示形式。 您可以使用旧版 API 访问文本视图，如下一节所示。  
  
## <a name="text-view-object"></a>文本视图对象  
 每个视图都与其自己的文本缓冲区关联，视图是缓冲区中数据的窗口。 下图显示了文本视图对象的关键接口，该对象由表示 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> 。  
  
 ![Visual Studio 文本视图对象](../extensibility/media/vstextview.gif "vstextview")  
文本视图对象  
  
 视图是在缓冲区中呈现文本的一种方法。 它包括自动换行和大纲显示等功能，以便在视图中看到的内容不是缓冲区中的文本的精确表示形式。  
  
 视图允许其他服务或进程截获传入命令并在其上操作之前对其执行操作。 最常见的服务是语言服务。 例如，语言服务可能需要截获 ENTER 键的命令，以提供自定义缩进行为或工具提示。  
  
## <a name="adding-functionality-to-the-text-view"></a>向文本视图添加功能  
 您可以通过处理特定击键来自定义文本视图行为。 若要截获击键，请 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 在对象上实现，并提供命令目标 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) 监视和截取命令。  
  
 文本视图对命令筛选器使用顺序体系结构。 新的命令筛选器 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 通过调用方法将) 添加到序列中的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 。  
  
 文本视图的事件通知是使用接口提供的 `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents` 。 在客户端对象上实现此接口可接收文本视图更改的通知。 使用文本视图上的接口向文本视图公开此接口， <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 以接收来自视图的更改通知。  
  
## <a name="see-also"></a>另请参阅  
 [使用旧版 API 更改视图设置](../extensibility/changing-view-settings-by-using-the-legacy-api.md)   
 [使用文本管理器监视全局设置](../extensibility/using-the-text-manager-to-monitor-global-settings.md)
