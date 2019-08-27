---
title: IDebugThread2::GetLogicalThread | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::GetLogicalThread
helpviewer_keywords:
- IDebugThread2::GetLogicalThread
ms.assetid: bce6230e-41d4-49b7-a050-2dde5efb6805
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f430ea7ba69ca55bc76543d853396e22b193cf02
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153055"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

调试引擎不会实现此方法。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetLogicalThread(   
   IDebugStackFrame2*     pStackFrame,  
   IDebugLogicalThread2** ppLogicalThread  
);  
```  
  
```csharp  
int GetLogicalThread(   
   IDebugStackFrame2        pStackFrame,  
   out IDebugLogicalThread2 ppLogicalThread  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pStackFrame`  
 [in][IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)对象，表示堆栈帧。  
  
 `ppLogicalThread`  
 [out]返回`IDebugLogicalThread2`接口，表示关联的逻辑线程。 调试引擎实现应设置为 null 值。  
  
## <a name="return-value"></a>返回值  
 调试引擎实现始终返回`E_NOTIMPL`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
