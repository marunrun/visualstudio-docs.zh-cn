---
title: IEnumDebugThreads2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 97bc8383f990f6c0c35a402f2ab36b2595d82a9e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68147688"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此 interfac 枚举当前调试会话中正在运行的线程。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugThreads2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口以表示程序中的线程列表。  
  
## <a name="notes-for-callers"></a>调用方说明  
 调用 [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md) 可获取此接口，该接口表示在进程中运行的所有程序中的所有线程的列表。 调用 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) 可获取表示程序中正在运行的线程列表的此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IEnumDebugThreads2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|检索枚举序列中指定数量的线程。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|跳过枚举序列中指定数量的线程。|  
|[重置](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|将枚举序列重置到开始处。|  
|[克隆](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|获取枚举器中的线程数。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 通常获取此接口以更新 " **线程** " 窗口以及获取列表的第一个线程，以便调用 [Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)、 [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)和 [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)   
 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)   
 [分步](../../../extensibility/debugger/reference/idebugprocess3-step.md)   
 [仍](../../../extensibility/debugger/reference/idebugprocess3-continue.md)   
 [执行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
