---
title: MemoryTypeEnum | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ded136da4d601fd7c11a10c21aac0c90864bc0bc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158134"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定要访问的内存类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum MemoryTypeEnum {  
   MemTypeCode,  
   MemTypeData,  
   MemTypeStack,  
   MemTypeAny = -1  
};  
```  
  
#### <a name="parameters"></a>参数  
 `MemTypeCode`  
 仅访问代码内存。  
  
 `MemTypeData`  
 访问数据或堆栈内存。  
  
 `MemTypeStack`  
 仅访问堆栈内存。  
  
 `MemTypeAny`  
 访问任何类型的内存。  
  
## <a name="remarks"></a>备注  
 此枚举中的值将传递给 [IDiaStackWalkHelper：： readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md) 方法，以限制对不同类型的内存的访问。  
  
## <a name="requirements"></a>要求  
 标头： cvconst  
  
## <a name="see-also"></a>另请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
