---
title: IDebugProcess3::GetDebugReason |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess3::GetDebugReason
helpviewer_keywords:
- IDebugProcess3::GetDebugReason
ms.assetid: f23fbabc-8b18-4278-bebf-4cdc7091513c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6223f72530b549e087511a3f26b7b864972a4dd6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202867"
---
# <a name="idebugprocess3getdebugreason"></a>IDebugProcess3::GetDebugReason
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法返回的原因进行调试时启动进程。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetDebugReason(  
   DEBUG_REASON* pReason  
);  
```  
  
```csharp  
int GetDebugReason(  
   out enum_DEBUG_REASON pReason  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pReason`  
 [out]返回一个值从[DEBUG_REASON](../../../extensibility/debugger/reference/debug-reason.md)枚举。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为将返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)   
 [DEBUG_REASON](../../../extensibility/debugger/reference/debug-reason.md)
