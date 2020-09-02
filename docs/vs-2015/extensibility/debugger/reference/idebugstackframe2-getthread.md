---
title: IDebugStackFrame2：： GetThread |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetThread
helpviewer_keywords:
- IDebugStackFrame2::GetThread
ms.assetid: cbeef85b-3dd7-4f97-adc2-c4d197d979fc
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9dd05e553ab5353b6ebf39970437c21c498caaff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62548087"
---
# <a name="idebugstackframe2getthread"></a>IDebugStackFrame2::GetThread
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取与堆栈帧关联的线程。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetThread (   
   IDebugThread2** ppThread  
);  
```  
  
```csharp  
int GetThread (   
   out IDebugThread2 ppThread  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppThread`  
 弄返回表示线程的 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
