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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203161"
---
# <a name="launch-based-attachment"></a>基于启动的附件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

基于启动的附件添加到某个程序是自动的。 托管程序的进程启动时通过 SDM，基于启动的附件遵循一个类似于手动附件方法的路径。 有关信息，请参阅[附加到程序](../../extensibility/debugger/attaching-to-the-program.md)。  
  
## <a name="the-attaching-process"></a>附加进程  
 主要区别是事件的顺序**附加**调用，请按如下所示：  
  
1. 发送**IDebugEngineCreateEvent2**到 SDM 事件对象。 有关详细信息，请参阅[发送事件](../../extensibility/debugger/sending-events.md)。  
  
2. 调用`IDebugProgram2::GetProgramId`方法**IDebugProgram2**接口传递给**附加**方法。  
  
3. 发送**IDebugProgramCreateEvent2**事件对象，以通知 SDM 的本地**IDebugProgram2**创建对象时用于表示 DE 程序。  
  
4. 发送[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)事件对象，以通知 SDM 启动的进程会创建一个新线程。  
  
## <a name="see-also"></a>请参阅  
 [发送必需的事件](../../extensibility/debugger/sending-the-required-events.md)   
 [启用要进行调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
