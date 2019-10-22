---
title: IJsDebugDataTarget：： FreeVirtualMemory 方法 |Microsoft Docs
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
ms.openlocfilehash: 835302249e95c89625c07c6d1ef3d7cbaf2905e8
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577610"
---
# <a name="ijsdebugdatatargetfreevirtualmemory-method"></a>IJsDebugDataTarget::FreeVirtualMemory 方法
释放和/或解除目标进程的虚拟地址空间内的内存区域。  
  
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
 中应释放内存的目标进程内的地址。  
  
 `size`  
 中要解除的字节数。 若要释放内存区域，此值必须为零。  
  
 `freeType`  
 中指示要执行的自由操作的类型。 这通常是 MEM_RELEASE （0x8000），它释放指定的页面区域。 操作完成后，页处于 "可用" 状态。 可以改为使用 MEM_DECOMMIT （0x4000）来解除页面，而无需释放它们。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 有关其他信息，请参阅 VirtualFree Win32 API。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)