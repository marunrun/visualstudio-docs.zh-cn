---
title: 旧 API 中的文本缓冲区事件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text buffer events
ms.assetid: 9be49e9f-1864-41c2-8a3c-f66895881341
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e82fa31ca435d0c850a4d9e75e927cff9613b046
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186403"
---
# <a name="text-buffer-events-in-the-legacy-api"></a>旧版 API 中的文本缓冲区事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本缓冲区对象发出几个不同的事件，使您可以对不同的情况做出响应。  
  
 使用旧版 API 时，应实现以下接口，以便接收文本缓冲区更改的通知。 使用文本缓冲区上的接口向文本缓冲区公开接口， `IConnectionPointContainer` 以接收来自缓冲区的行更改通知。 有关详细信息，请参阅 [如何：向旧 API 注册文本缓冲区事件](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)。 对于 `IVsTextStreamEvents` 或 `IVsTextLinesEvents` 接口，将分别在一维或二维坐标中返回更改。  
  
## <a name="text-buffer-interfaces"></a>文本缓冲区接口  
 下面是由文本缓冲区对象实现的接口。  
  
|接口|说明|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|启用复合操作 (即，) 中的单个撤消/重做单元分组的操作。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|启用由文本缓冲区管理的文档数据的持久性。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|提供基本服务;由许多客户端使用。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|使用二维坐标提供读写功能。 继承自 `IVsTextBuffer`。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|为缓冲区中的文本提供快速、面向流的顺序访问。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|使用一维坐标提供读写功能。 继承自 `IVsTextBuffer`。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|提供对属性的泛型集合的访问。 最重要的属性是缓冲区的名称或名字对象。 可以通过创建 GUID 并将其用作密钥，在缓冲区中存储你自己的随机数据。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|支持事件的连接点。|  
  
## <a name="text-buffer-event-interfaces"></a>文本缓冲区事件接口  
 下面是文本缓冲区事件通知的接口。  
  
|接口|说明|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferEvents>|当新语言服务与文本缓冲区关联时，通知客户端。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferDataEvents>|当初始化文本缓冲区和对文本缓冲区中的数据进行更改时通知客户端。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamEvents>|向客户端通知基础文本缓冲区在一维坐标中的更改。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents>|向客户端通知基础文本缓冲区在二维坐标中的更改。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserDataEvents>|通知客户端用户数据的更改。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>|通知客户端上一次提交手势触发事件，并提供文本范围更改。 `IVsPreliminaryTextChangeCommitEvents`响应 "撤消" 或 "重做" 命令时，不会触发接口。 仅对具有撤消管理器的缓冲区触发事件。 `IVsPreliminaryTextChangeCommitEvents` 在其他事件（如非常列表）之前激发，以确保在提交更改之前其他事件不会更改文本。 你的 VSPackage 必须监视 `IVsPreliminaryTextChangeCommitEvents` 接口或 `IVsFinalTextChangeCommitEvents` 接口，而不是两者都监视。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>|通知客户端上一次提交手势触发事件，并提供文本范围更改。 `IVsFinalTextChangeCommitEvents`响应 "撤消" 或 "重做" 命令时，不会触发接口。 仅对具有撤消管理器的缓冲区触发事件。 `IVsFinalTextChangeCommitEvents` 仅供语言服务或其他对编辑具有完全控制的对象使用。 你的 VSPackage 必须监视 `IVsPreliminaryTextChangeCommitEvents` 接口或 `IVsFinalTextChangeCommitEvents` 接口，而不是两者都监视。|  
  
## <a name="see-also"></a>另请参阅  
 [使用旧 API 访问文本缓冲区](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)   
 [如何：使用旧 API 注册文本缓冲区事件](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)
