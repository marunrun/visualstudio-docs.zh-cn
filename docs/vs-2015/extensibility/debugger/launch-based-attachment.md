---
title: 基于启动的附件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 09a6b39bef9ba6af098bf92d779a490e22492209
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203161"
---
# <a name="launch-based-attachment"></a>基于启动的附件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

程序的基于启动的附件是自动的。 当由 SDM 启动托管程序的进程时，基于启动的附件将遵循与手动附件方法类似的路径。 有关信息，请参阅 [附加到计划](../../extensibility/debugger/attaching-to-the-program.md)。  
  
## <a name="the-attaching-process"></a>附加进程  
 主要区别是 **连接** 调用后的事件序列，如下所示：  
  
1. 向 SDM 发送 **IDebugEngineCreateEvent2** 事件对象。 有关详细信息，请参阅 [发送事件](../../extensibility/debugger/sending-events.md)。  
  
2. `IDebugProgram2::GetProgramId`在传递给**Attach**方法的**IDebugProgram2**接口上调用方法。  
  
3. 发送 **IDebugProgramCreateEvent2** 事件对象，通知 SDM 创建了本地 **IDebugProgram2** 对象，以表示该程序被取消。  
  
4. 发送 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 事件对象来通知 SDM，为启动的进程创建新线程。  
  
## <a name="see-also"></a>另请参阅  
 [发送所需的事件](../../extensibility/debugger/sending-the-required-events.md)   
 [启用要进行调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
