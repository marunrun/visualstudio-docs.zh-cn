---
title: 如何：向旧 API 注册文本缓冲区事件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - register for text buffer events
ms.assetid: 5fc00ced-882c-4b48-b46c-1fa5a2469f94
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5f36e8dd780788d241e3c286b1bbbe581311b143
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204098"
---
# <a name="how-to-register-for-text-buffer-events-with-the-legacy-api"></a>如何：使用旧 API 注册文本缓冲区事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你使用旧版 API 访问文本缓冲区，则应注册文本缓冲区事件，如下面的过程所示。  
  
### <a name="to-advise-text-buffer-events"></a>建议文本缓冲区事件  
  
1. 从指向上某个接口的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ，调用指向的 `QueryInterface` 指针 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer.FindConnectionPoint%2A> 方法，并传入要注册的事件的接口 ID。  
  
     例如，如果要注册 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents> ，然后传入 IID_IVsTextLinesEvents 的接口 ID。  
  
     文本缓冲区返回指向 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 相应连接点对象的接口的指针。  
  
3. 使用此指针调用 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> 方法，并传入一个指针，该指针指向您要注册的事件接口的实现，例如 `IVsTextLinesEvents` 接口。  
  
     环境返回一个 cookie，然后可以使用该 cookie 通过调用方法停止对事件的侦听 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Unadvise%2A> 。  
  
## <a name="see-also"></a>另请参阅  
 [旧版 API 中的文本缓冲区事件](../extensibility/text-buffer-events-in-the-legacy-api.md)
