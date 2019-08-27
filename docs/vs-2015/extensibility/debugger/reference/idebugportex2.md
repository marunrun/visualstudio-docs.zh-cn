---
title: IDebugPortEx2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortEx2
helpviewer_keywords:
- IDebugPortEx2 interface
ms.assetid: 144724d0-38ee-4c9b-87ca-8a504371182b
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bb866c5cb968a4f03c718f04193026ac5308f7d4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681126"
---
# <a name="idebugportex2"></a>IDebugPortEx2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口允许程序和端口上运行的进程调试管理器 (SDM) 控件的会话。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPortEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 自定义端口提供程序实现此接口上实现的相同对象[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 SDM 调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上`IDebugPort2`接口，以获得此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugPortEx2`。  
  
|方法|描述|  
|------------|-----------------|  
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)|启动可执行文件。|  
|[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)|恢复过程的执行。|  
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugportex2-canterminateprocess.md)|确定是否可以终止进程。|  
|[TerminateProcess](../../../extensibility/debugger/reference/idebugportex2-terminateprocess.md)|终止进程。|  
|[GetPortProcessId](../../../extensibility/debugger/reference/idebugportex2-getportprocessid.md)|获取自身的端口的进程 ID。|  
|[GetProgram](../../../extensibility/debugger/reference/idebugportex2-getprogram.md)|获取与程序节点关联的程序。|  
  
## <a name="remarks"></a>备注  
 此接口是通常 SDM 和自定义端口供应商之间专用的。  
  
 如果需要，调试引擎 (DE) 可查看为此接口[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口传递给[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) ，并使用[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)启动程序。 但是，这不是必需的并且 DE 可以做它需要要执行的操作启动请求程序。  
  
## <a name="requirements"></a>要求  
 标头： portpriv.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
