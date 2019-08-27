---
title: IDebugBreakpointResolution2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointResolution2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 451d5bce-b9c1-48ff-beaa-2b4c3e1ceea0
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 031d8ffab94239c6169a61f3748172787267043c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160077"
---
# <a name="idebugbreakpointresolution2"></a>IDebugBreakpointResolution2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示用于描述绑定的断点的信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugBreakpointResolution2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 实现此接口作为断点的支持的一部分。 此接口提供了会话调试管理器时用户查看断点的属性使用的绑定断点的说明。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)返回此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugBreakpointResolution2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetBreakpointType](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|获取此解析由表示该断点的类型。|  
|[GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|获取描述此断点的断点解决方法信息。|  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)
