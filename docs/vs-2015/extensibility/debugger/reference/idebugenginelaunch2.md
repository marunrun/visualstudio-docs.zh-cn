---
title: IDebugEngineLaunch2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2
helpviewer_keywords:
- IDebugEngineLaunch2 interface
ms.assetid: 5eaf2ad8-3fbf-446e-b48b-5327ad3f5255
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ccbe76d800be035bc39caa477955b91bf21c074e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195671"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

由调试引擎使用 (DE) 启动和终止程序。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugEngineLaunch2 : IDebugEngine2  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 此接口是通过自定义 DE 实现的，如果它有启动无法完全通过自定义端口处理的进程的特殊要求。 当 DE 是解释器的一部分并且正在调试的进程是脚本时，通常会发生这种情况：解释器首先需要启动，然后加载并启动脚本。 端口可以启动解释器，但脚本可能需要特殊处理 (这是 DE) 的角色。 仅当启动自定义端口无法处理的程序的唯一要求时，才会实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 如果 SDM 可以使用 QueryInterface) 从 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) (接口获取此接口，则会话调试管理器 (sdm) 调用此接口。 如果可以获取此接口，则 SDM 知道该 DE 具有特殊要求，并调用此接口启动程序，而不是使端口启动该程序。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugEngineLaunch2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|通过取消方法启动进程。|  
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|继续执行进程。|  
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|确定进程是否可以终止。|  
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|终止进程。|  
  
## <a name="requirements"></a>要求  
 标头： Msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
