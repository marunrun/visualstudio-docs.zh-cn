---
title: IDebugThread2::Resume |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5bdec7338864926187b3d5056ffd2f2c4e1d7824
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152995"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

继续执行线程。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Resume (   
   DWORD *pdwSuspendCount  
);  
```  
  
```csharp  
int Resume (   
   out uint pdwSuspendCount  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pdwSuspendCount`  
 [out]恢复操作完成后返回的挂起计数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 每个调用此方法可将挂起计数直到中哪些时间达到 0，实际恢复执行。 此挂起计数显示在**线程**调试窗口。  
  
 对于每次调用此方法，必须有以前调用[挂起](../../../extensibility/debugger/reference/idebugthread2-suspend.md)方法。 挂起计数确定多少次`IDebugThread2::Suspend`到目前为止已调用方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md)
