---
title: IJsDebugDataTarget：： WriteMemory 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.WriteMemory
apilocation:
- jscript9diag.dll
ms.assetid: 0d3c04c3-9ef8-4842-a145-3d29bca75062
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 33cd23ad784e222f770dfd5c0e7c2d775aa55e42
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572414"
---
# <a name="ijsdebugdatatargetwritememory-method"></a>IJsDebugDataTarget::WriteMemory 方法
读取目标进程的内存。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT WriteMemory(  
   UINT64 address,  
   const BYTE *pMemory,  
   DWORD size  
);  
```  
  
#### <a name="parameters"></a>参数  
 `address`  
 中用于写入目标进程的内存的基址。  
  
 `pMemory`  
 中要写入指定进程的地址空间中的数据。  
  
 `size`  
 中要写入进程的字节数。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 在进行数据传输之前，系统将验证基址中的所有数据和指定大小的内存是否可供写入访问，如果不可访问，该函数将引发 E_JsDEBUG_INVALID_MEMORY_ADDRESS 错误。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)