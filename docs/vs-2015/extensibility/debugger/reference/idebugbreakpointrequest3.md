---
title: IDebugBreakpointRequest3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 50ea30c736a4606a7745e52057f2ca8f9afd2c5f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65673767"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示创建和绑定任何类型的断点所需的信息。 它是 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)的扩展。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugBreakpointRequest3 : IDebugBreakpointRequest2  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 会话调试管理器 (SDM) 通常实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 调试引擎 (DE) 通过在对[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)的调用中收到的 IDebugBreakpointRequest2 接口调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)来访问此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了从 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)继承的方法之外，接口还 `IDebugBreakpointRequest3` 公开以下方法。  
  
|方法|说明|  
|------------|-----------------|  
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|获取描述此断点请求的断点请求信息。|  
  
## <a name="remarks"></a>备注  
 此接口用于向通过 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构提供额外的信息。 此附加信息包括以 GUID) 形式提供的 DE 供应商 ID (、跟踪点的名称以及断点约束的名称。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
