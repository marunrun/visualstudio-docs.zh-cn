---
title: IDebugProgram2：： Step |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::Step
helpviewer_keywords:
- IDebugProgram2::Step
ms.assetid: e4c2ffce-9810-4088-8162-eac9ef04f2a9
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dd9d314865eb2051b67d7c127a6c5cc2395b1863
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387221"
---
# <a name="idebugprogram2step"></a>IDebugProgram2::Step
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

执行步骤。  
  
> [!NOTE]
> 不推荐使用此方法。 请改用[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Step(   
   IDebugThread2*  pThread,  
   STEPKIND        sk,  
   STEPUNIT        step  
);  
```  
  
```csharp  
int Step(   
   IDebugThread2  pThread,  
   enum_STEPKIND  sk,  
   enum_STEPUNIT  step  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pThread`  
 中一个[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，该对象表示正在逐步进行的线程。  
  
 `sk`  
 中[STEPKIND](../../../extensibility/debugger/reference/stepkind.md)枚举中的一个值，该值指定步骤的类型。  
  
 `step`  
 中[STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)枚举中的一个值，该值指定步骤的单位（例如，按语句或指令）。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果线程之间存在任何线程同步或通信，则程序中的其他线程应在单步执行时运行。  
  
> [!WARNING]
> 处理此调用时，不要将停止事件或即时（同步）事件发送到[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md);否则，调试器可能会停止响应。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
