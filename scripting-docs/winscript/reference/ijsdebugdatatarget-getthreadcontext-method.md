---
title: 'Ijsdebugdatatarget:: Getthreadcontext 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.GetThreadContext
apilocation:
- jscript9diag.dll
ms.assetid: faf2a689-6c49-4a7d-b5a6-2b323e2257a7
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d7904ef81eb900c6466069267101f30d89e362a1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62582828"
---
# <a name="ijsdebugdatatargetgetthreadcontext-method"></a>IJsDebugDataTarget::GetThreadContext 方法
给定线程的检索上下文。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetThreadContext(  
   DWORD threadId,  
   ULONG32 contextFlags,  
   ULONG32 contextSize,  
   void *pContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 `threadId`  
 [in]目标进程中运行的线程。  
  
 `contextFlags`  
 [in]指定上下文的标志。 这是与 （有关详细信息，请参阅 winnt.h，搜索 context_all） CONTEXT 的 ContextFlags 字段相同。  
  
 `contextSize`  
 [in]Pcontext 指定的缓冲区的大小。  
  
 `pContext`  
 [out]接收特定于平台的上下文结构到 pcontext 指定的缓冲区。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)