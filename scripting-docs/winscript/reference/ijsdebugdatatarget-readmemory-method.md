---
title: 'Ijsdebugdatatarget:: Readmemory 方法 |Microsoft Docs'
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
ms.openlocfilehash: 705fff3bf2d4be78897c18c5a4c61bd74a8c2230
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62582350"
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
 [in]要从其中读取目标进程的内存基址。  
  
 `flags`  
 [in]控制 ReadMemory 行为的标志。  
  
 `pBuffer`  
 [out]该缓冲区用于接收从目标进程的地址空间的内容。 在失败时，此缓冲区内容未指定。  
  
 `size`  
 [in]要从进程中读取的字节数。  
  
 `pBytesRead`  
 [out]指示从目标进程读取的字节数。 如果 JsDebugAllowPartialRead 明确，成功时此值将始终为输入大小完全相等。 如果指定 JsDebugAllowPartialRead，若成功，此值将大于零。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 成功和失败代码时返回 S_OK 用于任何错误。 如果地址不是有效，则返回 E_JsDEBUG_INVALID_MEMORY_ADDRESS。 有关详细信息，请参阅 JsDebugAllowPartialRead。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)