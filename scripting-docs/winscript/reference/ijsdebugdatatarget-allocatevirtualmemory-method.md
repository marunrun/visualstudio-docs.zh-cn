---
title: 'Ijsdebugdatatarget:: Allocatevirtualmemory 方法 |Microsoft Docs'
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
ms.openlocfilehash: c04bf21882ec39054c74f060eaa2c6f65ac0b4d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62583062"
---
# <a name="ijsdebugdatatargetallocatevirtualmemory-method"></a>IJsDebugDataTarget::AllocateVirtualMemory 方法
释放和/或提交目标过程虚拟地址空间内的内存区域。  
  
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
 [in]在目标进程应提交或保留的内存地址。 此值通常为的零，情况下，系统会选择地址。  
  
 `size`  
 [in]要分配，以字节为单位的内存区域的大小。 系统将自动向上舍入到下一步的页边界。  
  
 `allocationType`  
 [in]指示要执行分派的类型。 这通常是 MEM_COMMIT &#124; MEM_RESERVE (0x3000) 的保留和提交在一个步骤中的分配。  
  
 `pageProtection`  
 [in]页面并将其分配的内存保护的区域。 如果已提交页，可以指定内存保护常数 （例如，PAGE_READWRITE、 PAGE_EXECUTE） 之一。  
  
 `pAllocatedAddress`  
 [out]页分配的区域的基址。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 除非使用 mem_reset，该函数将初始化为零，分配的内存。 有关其他信息，请参阅 VirtualAlloc Win32 API。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)