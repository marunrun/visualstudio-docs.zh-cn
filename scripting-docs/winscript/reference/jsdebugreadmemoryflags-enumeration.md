---
title: JsDebugReadMemoryFlags 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- JsDebugReadMemoryFlags
apilocation:
- jscript9diag.dll
ms.assetid: 0d98d154-9cb1-49de-b2df-a2d029d343b7
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a1757678f20a01221ae46e1535d3190cd463d724
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571696"
---
# <a name="jsdebugreadmemoryflags-enumeration"></a>JsDebugReadMemoryFlags 枚举
读取内存时用于指定行为的标志。  
  
## <a name="syntax"></a>语法  
  
```cpp
enum JsDebugReadMemoryFlags{   None = 0,   JsDebugAllowPartialRead= 0x1} JsDebugReadMemoryFlags;  
```  
  
## <a name="members"></a>Members  
  
### <a name="values"></a>值  
  
|“属性”|描述|  
|----------|-----------------|  
|`JsDebugAllowPartialRead`|指示调用方希望读取操作在部分内存读取成功时才会成功。 如果已设置此设置，则仅当 "Address" 无效时才会引发 E_JsDEBUG_INVALID_MEMORY_ADDRESS 错误。 如果清除此标志，则在请求的内存的任何部分无法读取时，将引发 E_JsDEBUG_INVALID_MEMORY_ADDRESS 错误。|  
|`None`|指示调用方需要 ReadMemory 的默认行为。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)