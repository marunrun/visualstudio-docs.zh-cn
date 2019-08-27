---
title: IRemoteDebugApplicationEvents 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplicationEvents interface
ms.assetid: 9626519e-910c-48e0-ae99-c711ce6628fd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 052a408d6e92066c14617f46f722d3e603985195
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943811"
---
# <a name="iremotedebugapplicationevents-interface"></a>IRemoteDebugApplicationEvents 接口
`IRemoteDebugApplicationEvents`接口是调试应用程序提供的事件接口。 此接口是始终从内调用调试器线程。  
  
 除了继承的方法之外`IUnknown`，则`IRemoteDebugApplicationEvents`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IRemoteDebugApplicationEvents::OnConnectDebugger](../../winscript/reference/iremotedebugapplicationevents-onconnectdebugger.md)|句柄的调试器连接事件。|  
|[IRemoteDebugApplicationEvents::OnDisconnectDebugger](../../winscript/reference/iremotedebugapplicationevents-ondisconnectdebugger.md)|句柄的调试器断开连接事件。|  
|[IRemoteDebugApplicationEvents::OnSetName](../../winscript/reference/iremotedebugapplicationevents-onsetname.md)|处理设置名称事件。|  
|[IRemoteDebugApplicationEvents::OnDebugOutput](../../winscript/reference/iremotedebugapplicationevents-ondebugoutput.md)|处理调试器输出事件。|  
|[IRemoteDebugApplicationEvents::OnClose](../../winscript/reference/iremotedebugapplicationevents-onclose.md)|处理应用程序关闭事件。|  
|[IRemoteDebugApplicationEvents::OnEnterBreakPoint](../../winscript/reference/iremotedebugapplicationevents-onenterbreakpoint.md)|处理用于输入断点的事件。|  
|[IRemoteDebugApplicationEvents::OnLeaveBreakPoint](../../winscript/reference/iremotedebugapplicationevents-onleavebreakpoint.md)|处理的事件保留断点。|  
|[IRemoteDebugApplicationEvents::OnCreateThread](../../winscript/reference/iremotedebugapplicationevents-oncreatethread.md)|处理在创建线程事件。|  
|[IRemoteDebugApplicationEvents::OnDestroyThread](../../winscript/reference/iremotedebugapplicationevents-ondestroythread.md)|处理线程销毁事件。|  
|[IRemoteDebugApplicationEvents::OnBreakFlagChange](../../winscript/reference/iremotedebugapplicationevents-onbreakflagchange.md)|处理中断标志更改时发生的事件。|