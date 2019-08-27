---
title: 通知端口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8cf3969dda783882f24d02a748f345cdb66fe413
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63410073"
---
# <a name="notifying-the-port"></a>通知端口
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

启动后一个程序，该端口必须得到通知，请按如下所示：  
  
1. 当一个端口收到新的程序节点时，将回复到调试会话发送程序创建事件。 事件将携带的表示该程序的接口。  
  
2. 调试会话查询可以将附加到调试引擎 (DE) 的标识符的程序。  
  
3. 调试会话进行检查以查看 DE 是否为该程序允许 DEs 列表上。 调试会话获取此列表从解决方案的活动程序设置，最初传递给它的调试包。  
  
    DE 必须位于允许列表中，否则设备将不会附加到程序。  
  
   以编程方式，当一个端口先接收新的程序节点，它会创建[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)接口来表示该程序。  
  
> [!NOTE]
> 不应与混淆这`IDebugProgram2`接口更高版本创建的调试引擎 (DE)。  
  
 该端口将发送[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)程序创建事件返回到会话调试管理器 (SDM) 通过 COM`IConnectionPoint`接口。  
  
> [!NOTE]
> 不应与混淆这`IDebugProgramCreateEvent2`接口，由 DE 发出的更高版本。  
  
 事件接口本身，以及该端口将发送[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)， [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)，并[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)接口，表示该端口，处理，并编程，分别。 SDM 调用[IDebugProgram2::GetEngineInfo](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)要获取可以调试程序，DE GUID。 从最初获取 GUID [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口。  
  
 SDM 检查 DE 是否允许 DEs 列表上。 SDM 从解决方案的活动程序设置，最初传递给它的调试包中获取此列表。 DE 必须位于允许列表中，否则将不会附加到该程序。  
  
 一旦 DE 该标识已知，SDM 已准备好将其附加到该程序。  
  
## <a name="see-also"></a>请参阅  
 [启动程序](../../extensibility/debugger/launching-a-program.md)   
 [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md)   
 [调试任务](../../extensibility/debugger/debugging-tasks.md)
