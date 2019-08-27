---
title: IRemoteDebugApplication 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplication interface
ms.assetid: 96bf2a3f-049f-46ba-86ad-57fc184343a2
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2a231818def210f7c88ab031059f8561c67b33d1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944238"
---
# <a name="iremotedebugapplication-interface"></a>IRemoteDebugApplication 接口
表示正在运行的应用程序。 它不需要以与操作系统进程相对应。 通常情况下，调试器以用于调试的应用程序目标。 进程调试管理器通常实现应用程序对象。  
  
 除了继承的方法之外`IUnknown`，则`IRemoteDebugApplication`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IRemoteDebugApplication::ResumeFromBreakPoint](../../winscript/reference/iremotedebugapplication-resumefrombreakpoint.md)|继续当前断点的应用程序。|  
|[IRemoteDebugApplication::CauseBreak](../../winscript/reference/iremotedebugapplication-causebreak.md)|导致应用程序在最早的机会在调试器中中断。|  
|[IRemoteDebugApplication::ConnectDebugger](../../winscript/reference/iremotedebugapplication-connectdebugger.md)|将调试器连接到此应用程序。|  
|[IRemoteDebugApplication::DisconnectDebugger](../../winscript/reference/iremotedebugapplication-disconnectdebugger.md)|断开当前的调试器与应用程序的连接。|  
|[IRemoteDebugApplication::GetDebugger](../../winscript/reference/iremotedebugapplication-getdebugger.md)|返回当前调试器连接到该应用程序。|  
|[IRemoteDebugApplication::CreateInstanceAtApplication](../../winscript/reference/iremotedebugapplication-createinstanceatapplication.md)|调试器 IDE，正在运行的进程外应用程序，在应用程序进程中创建对象提供一种机制。|  
|[IRemoteDebugApplication::QueryAlive](../../winscript/reference/iremotedebugapplication-queryalive.md)|指示该应用程序是否响应。|  
|[IRemoteDebugApplication::EnumThreads](../../winscript/reference/iremotedebugapplication-enumthreads.md)|枚举已知要与应用程序相关联的所有线程。|  
|[IRemoteDebugApplication::GetName](../../winscript/reference/iremotedebugapplication-getname.md)|返回此应用程序节点的名称。|  
|[IRemoteDebugApplication::GetRootNode](../../winscript/reference/iremotedebugapplication-getrootnode.md)|返回与该应用程序相关联的所有节点将都添加在其下的应用程序节点。|  
|[IRemoteDebugApplication::EnumGlobalExpressionContexts](../../winscript/reference/iremotedebugapplication-enumglobalexpressioncontexts.md)|枚举此应用程序中运行的所有语言的全局表达式上下文。|