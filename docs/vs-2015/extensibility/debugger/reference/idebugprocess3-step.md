---
title: IDebugProcess3：： Step |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess3::Step
helpviewer_keywords:
- IDebugProcess3::Step
ms.assetid: 6ad9094c-27cc-4927-8a7c-1b4d97b2e436
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5069a40f4e3ea4b1fba74c8133a18b46f2b3f2d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86386220"
---
# <a name="idebugprocess3step"></a>IDebugProcess3::Step
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

使进程单步执行一条指令或语句。  
  
> [!NOTE]
> 应使用此方法而不是 [步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT Step(  
   IDebugThread2* pThread,  
   STEPKIND       sk,  
   STEPUNIT       step,  
);  
```  
  
```csharp  
int Step(  
   IDebugThread2 pThread,   
   enum_STEPKIND sk,   
   enum_STEPUNIT step  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pThread`  
 中一个 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象，表示正在逐步进行的线程。  
  
 `sk`  
 中 [STEPKIND](../../../extensibility/debugger/reference/stepkind.md) 值之一。  
  
 `step`  
 中 [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md) 值之一。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果线程之间存在任何线程同步或通信，则进程中的其他线程应在单步执行时运行。  
  
 **警告** 处理此调用时，不要将停止事件或立即 (同步) 事件发送到 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) ;否则，调试器可能会停止响应。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [STEPKIND](../../../extensibility/debugger/reference/stepkind.md)   
 [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)   
 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
