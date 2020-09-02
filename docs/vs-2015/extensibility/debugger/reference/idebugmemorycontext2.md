---
title: IDebugMemoryContext2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2
helpviewer_keywords:
- IDebugMemoryContext2 interface
ms.assetid: 3a544c8b-11dc-46bb-8549-261e4ac5bbc4
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6f5a0533e2f7ce50dce7ccdf1285e4ab28a4b7a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146356"
---
# <a name="idebugmemorycontext2"></a>IDebugMemoryContext2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示运行正在调试的程序的计算机的地址空间中的位置。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugMemoryContext2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口以表示内存中的地址。  
  
## <a name="notes-for-callers"></a>调用方说明  
 对 [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) 或 [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md) 的调用返回此接口。 此外，在应用适当的算术运算后，对添加和[减去](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)的调用[将](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)返回此接口的新副本。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugMemoryContext2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[GetName](../../../extensibility/debugger/reference/idebugmemorycontext2-getname.md)|获取此上下文的用户可显示名称。|  
|[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)|获取描述此上下文的信息。|  
|[添加](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)|将指定的值添加到当前上下文的地址，以创建新的上下文。|  
|[减去](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)|从当前上下文的地址减去指定的值以创建新的上下文。|  
|[比较](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)|按比较标志所指示的方式对两个上下文进行比较。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 的 " **内存** " 窗口调用 [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) 来获取 `IDebugMemoryContext2` 包含用于内存地址的计算表达式的接口。 然后，将此上下文传递给 [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) 和 [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md) ，以指定要读取或写入的地址。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)   
 [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)   
 [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)   
 [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)
