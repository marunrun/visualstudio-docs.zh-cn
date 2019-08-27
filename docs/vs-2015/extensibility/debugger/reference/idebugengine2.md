---
title: IDebugEngine2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0c011a530bbd4323546257a40334a4b8a0f57bdb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195912"
---
# <a name="idebugengine2"></a>IDebugEngine2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示调试引擎 (DE)。 它用于从创建到设置，然后清除异常断点管理调试会话的各个方面。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugEngine2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 此接口由自定义部署来管理调试程序的实现。 此接口必须由 DE 实现。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口由会话调试管理器 (SDM) 来管理调试会话，包括管理异常、 创建断点，以及响应发送的 DE 的同步事件的调用。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugEngine2`。  
  
|方法|描述|  
|------------|-----------------|  
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|创建 DE 正在调试的所有程序的枚举器。|  
|[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)|将 DE 附加到程序。|  
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|在 DE 中创建挂起断点。|  
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|指定 DE 应如何处理给定的异常。|  
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|以便不再由调试引擎中移除指定的异常。|  
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|删除的异常 IDE 已设置为特定的运行时体系结构或语言的列表。|  
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|获取 DE 的 GUID。|  
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|通知已异常终止指定的程序且 DE 应清理对该程序的所有引用，并发送程序 DE 销毁事件。|  
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|由 SDM，指示同步调试事件，以前发送到 SDM，DE 已接收并处理调用。|  
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|设置 DE 的区域设置。|  
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|由 DE 使用当前设置的注册表根目录。|  
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|设置指标。|  
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|所有此 DE 正在调试的程序停止执行其线程之一尝试运行下一次的请求。|  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)
