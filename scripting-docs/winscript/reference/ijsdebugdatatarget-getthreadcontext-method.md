---
title: IJsDebugDataTarget：： GetThreadContext 方法 |Microsoft Docs
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
ms.openlocfilehash: da5722553b448605129adcf32cfaa52e2dc76352
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577661"
---
# <a name="ijsdebugdatatargetgetthreadcontext-method"></a>IJsDebugDataTarget::GetThreadContext 方法
检索给定线程的上下文。  
  
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
 中在目标进程中运行的线程。  
  
 `contextFlags`  
 中指定上下文标志。 这与上下文的 ContextFlags 字段相同（有关详细信息，请参阅 winnt，搜索 CONTEXT_ALL）。  
  
 `contextSize`  
 中PContext 指定的缓冲区大小。  
  
 `pContext`  
 弄接收由 pContext 指定的缓冲区中特定于平台的上下文结构。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)