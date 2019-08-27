---
title: IDebugProgram2::Step | Microsoft Docs
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
ms.openlocfilehash: 0473cf7061cb18dad569910af5214742ba774a87
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445779"
---
# <a name="idebugprogram2step"></a>IDebugProgram2::Step
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

执行一个步骤。  
  
> [!NOTE]
> 已弃用此方法。 使用[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)方法相反。  
  
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
 [in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示正在单步执行的线程。  
  
 `sk`  
 [in]中的值[STEPKIND](../../../extensibility/debugger/reference/stepkind.md)枚举，用于指定类型的步骤。  
  
 `step`  
 [in]中的值[STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)枚举，用于指定步骤的单元 （例如，通过语句或指令）。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果没有任何线程同步或线程之间的通信，当特定线程单步执行时应运行程序中的其他线程。  
  
> [!WARNING]
> 不发送停止事件或将即时 （同步） 事件与[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)时处理此调用; 否则调试器可能会挂起。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
