---
title: IRemoteDebugApplicationThread 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplicationThread interface
ms.assetid: 062bb997-7b9e-4945-bfbe-d5b92d5cb707
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fd0574fe6093c6d53a63dfbbc97a7a313eaedc5f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788031"
---
# <a name="iremotedebugapplicationthread-interface"></a>IRemoteDebugApplicationThread 接口
表示特定应用程序中的执行线程。  
  
 除了继承的方法之外`IUnknown`，则`IRemoteDebugApplicationThread`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IRemoteDebugApplicationThread::GetSystemThreadId](../../winscript/reference/iremotedebugapplicationthread-getsystemthreadid.md)|返回与线程关联的依赖于操作系统的标识符。|  
|[IRemoteDebugApplicationThread::GetApplication](../../winscript/reference/iremotedebugapplicationthread-getapplication.md)|返回与此线程关联的应用程序对象。|  
|[IRemoteDebugApplicationThread::EnumStackFrames](../../winscript/reference/iremotedebugapplicationthread-enumstackframes.md)|返回与此线程的堆栈帧的枚举器。|  
|[IRemoteDebugApplicationThread::GetDescription](../../winscript/reference/iremotedebugapplicationthread-getdescription.md)|获取描述和此线程的状态。|  
|[IRemoteDebugApplicationThread::SetNextStatement](../../winscript/reference/iremotedebugapplicationthread-setnextstatement.md)|继续为给定的代码上下文，尽可能地接近给定帧的上下文中的强制执行。|  
|[IRemoteDebugApplicationThread::GetState](../../winscript/reference/iremotedebugapplicationthread-getstate.md)|获取此线程的状态。|  
|[IRemoteDebugApplicationThread::Suspend](../../winscript/reference/iremotedebugapplicationthread-suspend.md)|将线程挂起。|  
|[IRemoteDebugApplicationThread::Resume](../../winscript/reference/iremotedebugapplicationthread-resume.md)|恢复线程。|  
|[IRemoteDebugApplicationThread::GetSuspendCount](../../winscript/reference/iremotedebugapplicationthread-getsuspendcount.md)|返回线程的挂起计数。|