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
ms.openlocfilehash: c908fdbf17b13b84355dff208b7f3106bfc72087
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830457"
---
# <a name="jsdebugreadmemoryflags-enumeration"></a>JsDebugReadMemoryFlags 枚举
读取内存时用于指定行为的标志。  
  
## <a name="syntax"></a>语法  
  
```cpp
enum JsDebugReadMemoryFlags{   None = 0,   JsDebugAllowPartialRead= 0x1} JsDebugReadMemoryFlags;  
```  
  
## <a name="members"></a>成员  
  
### <a name="values"></a>值  
  
|名称|描述|  
|----------|-----------------|  
|`JsDebugAllowPartialRead`|指示调用方想要读取的操作，如果只有部分内存读取成功。 如果此设置，E_JsDEBUG_INVALID_MEMORY_ADDRESS 错误将仅引发 Address 是否无效。 如果清除此标志，如果请求的任何的内存部分是不可读，将会引发 E_JsDEBUG_INVALID_MEMORY_ADDRESS 错误。|  
|`None`|指示调用方希望 ReadMemory 的默认行为。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)