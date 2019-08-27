---
title: EVENTATTRIBUTES |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3026845be9aa6623d6c5cd42406385e8c5c2a11e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149377"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定的事件属性。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_EVENTATTRIBUTES {   
   EVENT_ASYNCHRONOUS          = 0x0000,  
   EVENT_SYNCHRONOUS           = 0x0001,  
   EVENT_STOPPING              = 0x0002,  
   EVENT_ASYNC_STOP            = 0x0002,  
   EVENT_SYNC_STOP             = 0x0003,  
   EVENT_IMMEDIATE             = 0x0004,  
   EVENT_EXPRESSION_EVALUATION = 0x0008  
};  
typedef DWORD EVENTATTRIBUTES;  
```  
  
```csharp  
public enum enum_EVENTATTRIBUTES {   
   EVENT_ASYNCHRONOUS          = 0x0000,  
   EVENT_SYNCHRONOUS           = 0x0001,  
   EVENT_STOPPING              = 0x0002,  
   EVENT_ASYNC_STOP            = 0x0002,  
   EVENT_SYNC_STOP             = 0x0003,  
   EVENT_IMMEDIATE             = 0x0004,  
   EVENT_EXPRESSION_EVALUATION = 0x0008  
};  
```  
  
## <a name="members"></a>成员  
 EVENT_ASYNCHRONOUS  
 指示事件是异步的需要该事件没有收到回复。  
  
 EVENT_SYNCHRONOUS  
 指示事件是同步的通过答复[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)。  
  
 EVENT_STOPPING  
 指示这是一个停止事件。 必须使用组合`EVENT_ASYNCHRONOUS`或`EVENT_SYNCHRONOUS`。  
  
 EVENT_ASYNC_STOP  
 表示异步停止事件。 当前没有此类事件。 此标志只是一个占位符。  
  
 EVENT_SYNC_STOP  
 指示同步停止事件 (的组合`EVENT_SYNCHRONOUS`和`EVENT_STOPPING`)。 发送 stopping 事件时，调试引擎 (DE) 使用此值。 通过调用进行答复[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)，[步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)，或[继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)。  
  
 EVENT_IMMEDIATE  
 指示将立即并以同步方式发送到 IDE 的事件。 此标志结合了等其他标志`EVENT_ASYNCHRONOUS`， `EVENT_SYNCHRONOUS`，或`EVENT_SYNC_STOP`来指示类型的事件，并在已知 （如果有） 的回复机制。  
  
 EVENT_EXPRESSION_EVALUATION  
 该事件为表达式计算的结果。  
  
## <a name="remarks"></a>备注  
 这些值将按传递`dwAttrib`的参数[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法。  
  
 可能的按位组合这些值`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
