---
title: 旧版 API 中的文本缓冲区事件 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186403"
---
# <a name="text-buffer-events-in-the-legacy-api"></a>旧版 API 中的文本缓冲区事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本缓冲区对象会发出多个不同的事件，您可以对不同的情况下作出响应。  
  
 当使用传统的 API 时，应以接收通知的文本缓冲区更改来实现以下接口。 显示文本缓冲区使用的接口`IConnectionPointContainer`接口上要接收通知的行的文本缓冲区更改从缓冲区。 有关详细信息，请参阅[如何：为使用旧 API 的文本缓冲区事件注册](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)。 情况下`IVsTextStreamEvents`或`IVsTextLinesEvents`接口，则返回的更改以任一一或或双三维坐标，分别。  
  
## <a name="text-buffer-interfaces"></a>文本缓冲区接口  
 以下是实现文本缓冲区对象的接口。  
  
|接口|描述|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|可以创建复合操作 （即，在撤消/重做单个单元进行分组的操作）。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|使文档数据管理的文本缓冲区的持久性。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|提供基本服务;由多个客户端。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|提供了读取和写入功能使用二维坐标。 继承自 `IVsTextBuffer`。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|提供快速、 面向流的顺序访问缓冲区中的文本。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|提供了读取和写入功能使用一维的坐标。 继承自 `IVsTextBuffer`。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|提供对属性的泛型集合的访问。 最重要属性是缓冲区的名称或的名字对象。 通过创建 GUID 并使用它作为键，可以使用此接口在缓冲区中存储自己的随机数据。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|支持连接点的事件。|  
  
## <a name="text-buffer-event-interfaces"></a>文本缓冲区事件接口  
 以下是文本缓冲区事件通知的接口。  
  
|接口|描述|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferEvents>|通知客户端时提供新语言服务是与文本缓冲区相关联。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferDataEvents>|初始化文本缓冲区和文本缓冲区中的数据发生更改时通知客户端。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamEvents>|通知客户端的一维坐标中的基础文本缓冲区更改。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents>|通知客户端的二维坐标中的基础文本缓冲区更改。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserDataEvents>|通知客户端的对用户数据的更改。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>|通知客户端的最后一个提交手势以触发该事件，并提供文本更改的范围。 `IVsPreliminaryTextChangeCommitEvents`接口不触发响应撤消或重做命令。 针对具有撤消管理器的缓冲区的仅触发事件。 `IVsPreliminaryTextChangeCommitEvents` 触发之前其他事件，如整齐排列，这样可确保其他事件不会更改文本之前在提交更改。 你的 VSPackage 必须监视任一`IVsPreliminaryTextChangeCommitEvents`接口或`IVsFinalTextChangeCommitEvents`接口，但不可同时使用两者。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>|通知客户端的最后一个提交手势以触发该事件，并提供文本更改的范围。 `IVsFinalTextChangeCommitEvents`接口不触发响应撤消或重做命令。 针对具有撤消管理器的缓冲区的仅触发事件。 `IVsFinalTextChangeCommitEvents` 旨在仅由语言服务或具有对编辑的完全控制的其他对象的使用。 你的 VSPackage 必须监视任一`IVsPreliminaryTextChangeCommitEvents`接口或`IVsFinalTextChangeCommitEvents`接口，但不可同时使用两者。|  
  
## <a name="see-also"></a>请参阅  
 [使用旧版 API 访问的文本缓冲区](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)   
 [如何：使用旧 API 注册文本缓冲区事件](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)
