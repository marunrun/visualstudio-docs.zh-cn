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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195671"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

由调试引擎 (DE) 来启动和终止程序。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugEngineLaunch2 : IDebugEngine2  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 如果它具有用于启动一个过程，不能完全由自定义端口处理的特殊要求，自定义 DE 被实现此接口。 这通常是这种情况，DE 属于解释器和正在调试的进程是一个脚本时： 解释器需要首先，启动，然后加载并启动该脚本。 一个端口可以启动解释程序，但该脚本可能需要特殊处理 （这是其中 DE 具有的角色）。 仅在没有启动自定义端口不能处理程序的唯一要求被实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口由会话调试管理器 (SDM) 如果 SDM 可以获取此接口从调用[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口 （使用 QueryInterface）。 如果可以获取此接口，SDM 知道 DE 有特殊的要求，并且调用此接口来启动程序而不是启动管理器的端口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugEngineLaunch2`。  
  
|方法|描述|  
|------------|-----------------|  
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|通过 DE 启动进程。|  
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|恢复进程执行。|  
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|确定是否可以终止进程。|  
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|终止进程。|  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
