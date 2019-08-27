---
title: IDebugProgram2::Continue | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::Continue
helpviewer_keywords:
- IDebugProgram2::Continue
ms.assetid: e5a6e02a-d21b-4a03-a034-e8de1f71ce2e
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f28379d202a59ca2bdf9bfc7eb1185dee343accf
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63426299"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将继续运行此程序从已停止状态。 保留任何以前的执行状态 （如步骤），然后再次执行该程序开始。  
  
> [!NOTE]
> 已弃用此方法。 使用[继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)方法相反。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Continue(   
   IDebugThread2* pThread  
);  
```  
  
```csharp  
int Continue(   
   IDebugThread2 pThread  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pThread`  
 [in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)表示的线程的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 在此程序而不考虑正在调试程序数，或哪些程序生成 stopping 事件上调用此方法。 实现必须保留以前的执行状态 （如步骤），并继续执行，就好像它永远不会有停止之前完成其前面的执行。 也就是说，如果此程序中的线程执行逐过程操作，并已停止，因为其他程序中停止，并调用该方法然后，程序必须完成原始逐过程操作。  
  
> [!WARNING]
> 不发送停止事件或将即时 （同步） 事件与[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)时处理此调用; 否则调试器可能会挂起。  
  
## <a name="see-also"></a>请参阅  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
