---
title: IJsDebugDataTarget：： AllocateVirtualMemory 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.AllocateVirtualMemory
apilocation:
- jscript9diag.dll
ms.assetid: 1d3a77b0-c1de-4a0c-a759-3e0c68fd96dd
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 30ad8a3eb277823271fbfb4c2e10364b8602775c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577646"
---
# <a name="ijsdebugdatatargetallocatevirtualmemory-method"></a>IJsDebugDataTarget::AllocateVirtualMemory 方法
保留和/或提交目标进程的虚拟地址空间内的内存区域。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AllocateVirtualMemory(  
   UINT64 address,  
   DWORD size,  
   DWORD allocationType,  
   DWORD pageProtection,  
   UINT64 *pAllocatedAddress  
);  
```  
  
#### <a name="parameters"></a>参数  
 `address`  
 中目标进程中应提交或保留内存的地址。 此值通常为零，在这种情况下，系统会选择一个地址。  
  
 `size`  
 中要分配的内存区域的大小（以字节为单位）。 系统将自动向上舍入到下一个页面边界。  
  
 `allocationType`  
 中指示要执行的分配的类型。 这通常是 MEM_COMMIT &#124; MEM_RESERVE （0x3000），可在一步中保留并提交分配。  
  
 `pageProtection`  
 中要分配的页面区域的内存保护。 如果正在提交页面，可以指定任何一个内存保护常量（例如，PAGE_READWRITE、PAGE_EXECUTE）。  
  
 `pAllocatedAddress`  
 弄已分配的页面区域的基址。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 函数将它分配的内存初始化为零，除非使用 MEM_RESET。 有关其他信息，请参阅 VirtualAlloc Win32 API。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)