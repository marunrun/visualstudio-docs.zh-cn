---
title: IJsDebugDataTarget：： GetTlsValue 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.GetTlsValue
apilocation:
- jscript9diag.dll
ms.assetid: db575be9-7b24-45c5-9008-e4f2f76d6757
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eecf9acf370656d5310a03d68ed74e10671a0bc2
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577608"
---
# <a name="ijsdebugdatatargetgettlsvalue-method"></a>IJsDebugDataTarget::GetTlsValue 方法
对于正在调试的线程，将检索指定 TLS 索引的线程本地存储（TLS）槽中的值。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetTlsValue(  
   DWORD threadId,  
   UINT32 tlsIndex,  
   UINT64 *pValue  
);  
```  
  
#### <a name="parameters"></a>参数  
 `threadId`  
 中要从其读取的目标进程中运行的线程。  
  
 `tlsIndex`  
 中当目标进程调用 TlsAlloc 函数时分配的 TLS 索引。  
  
 `pValue`  
 弄已存储在线程的 TLS 槽中的指针大小的值。 如果目标线程为32位，则此值的32位将为零。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 进程的每个线程都有自己的针对每个 TLS 索引的槽。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)