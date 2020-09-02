---
title: IDebugEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEvent2
helpviewer_keywords:
- IDebugEvent2 interface
ms.assetid: de3d714d-96fb-4e12-b66b-a75391472153
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f663be5910b342a6adba5da0b84d7e0d80cacc10
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695417"
---
# <a name="idebugevent2"></a>IDebugEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口用于传达关键调试信息，例如在断点处停止，以及非关键信息，如调试消息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 和自定义端口供应商在与所有其他事件接口相同的对象上实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 使用接口 ID (IID) 提供给 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) 或 [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)的参数，会话调试管理器 (SDM) 调用接口上的 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) `IDebugEvent2` 以获取适当的事件接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugEvent2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)|获取此调试事件的特性。|  
  
## <a name="remarks"></a>备注  
 更具体的事件接口（如 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)）不是从 IDebugEvent2 接口派生的，而是作为与相同的对象上的单独接口实现的 `IDebugEvent2` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [引发](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
