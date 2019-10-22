---
title: IJsDebugDataTarget：： ReadMemory 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.ReadMemory
apilocation:
- jscript9diag.dll
ms.assetid: 664e0f7d-2007-45f4-b993-36fe8b1944e5
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 84da36433cf3546b34d3e044bb113916c9798117
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572432"
---
# <a name="ijsdebugdatatargetreadmemory-method"></a>IJsDebugDataTarget::ReadMemory 方法
读取目标进程的内存。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ReadMemory(  
   UINT64 address,  
   JsDebugReadMemoryFlags flags,  
   BYTE *pBuffer,  
   DWORD size,  
   DWORD *pBytesRead  
);  
```  
  
#### <a name="parameters"></a>参数  
 `address`  
 中从中读取目标进程的内存的基址。  
  
 `flags`  
 中控制 ReadMemory 行为的标志。  
  
 `pBuffer`  
 弄接收目标进程的地址空间中的内容的缓冲区。 出现故障时，未指定此缓冲区的内容。  
  
 `size`  
 中要从进程中读取的字节数。  
  
 `pBytesRead`  
 弄指示从目标进程中读取的字节数。 如果 JsDebugAllowPartialRead 清晰，此值将始终与输入大小完全相等。 如果指定了 JsDebugAllowPartialRead，则在成功时，此值将大于零。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 成功时返回 S_OK，错误代码用于任何错误。 如果地址无效，则返回 E_JsDEBUG_INVALID_MEMORY_ADDRESS。 有关详细信息，请参阅 JsDebugAllowPartialRead。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)