---
title: 'Ijsdebugdatatarget:: Freevirtualmemory 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.FreeVirtualMemory
apilocation:
- jscript9diag.dll
ms.assetid: ea54bad3-9ae3-436b-974d-70fc7fffefd6
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bf450c03d996a47f9dcd00899ddee46b75d6df32
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62583036"
---
# <a name="ijsdebugdatatargetfreevirtualmemory-method"></a>IJsDebugDataTarget::FreeVirtualMemory 方法
释放和/或解除目标过程虚拟地址空间内的内存区域。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT FreeVirtualMemory(  
   UINT64 address,  
   DWORD size,  
   DWORD freeType  
);  
```  
  
#### <a name="parameters"></a>参数  
 `address`  
 [in]在目标进程应释放内存内的地址。  
  
 `size`  
 [in]要解除的字节数。 若要释放的内存区域，此值必须为零。  
  
 `freeType`  
 [in]指示要执行的可用操作的类型。 这通常是 MEM_RELEASE (0x8000)，会释放指定的页面区域。 操作后，在页处于可用状态。 可以改为使用 MEM_DECOMMIT (0x4000)，解除页，而不释放它们。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 有关其他信息，请参阅 VirtualFree Win32 API。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)