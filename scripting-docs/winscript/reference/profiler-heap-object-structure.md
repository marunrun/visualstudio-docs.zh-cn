---
title: PROFILER_HEAP_OBJECT 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9f35362c-6856-4cfb-b990-031a156a58eb
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a1652c6ebffff88782ffcc879158a5142f22395d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823809"
---
# <a name="profilerheapobject-structure"></a>PROFILER_HEAP_OBJECT 结构
表示堆对象收集[IActiveScriptProfilerControl3::EnumHeap 方法](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct _PROFILER_HEAP_OBJECT  
{  
    UINT size;    union {        PROFILER_HEAP_OBJECT_ID objectId;        PROFILER_EXTERNAL_OBJECT_ADDRESS externalObjectAddress;    };    PROFILER_HEAP_OBJECT_NAME_ID typeNameId;    USHORT flags;     USHORT optionalInfoCount;} PROFILER_HEAP_OBJECT;  
```  
  
## <a name="members"></a>成员  
  
|成员|类型|描述|  
|------------|----------|-----------------|  
|objectId|[PROFILER_HEAP_OBJECT_ID 类型](../../winscript/reference/profiler-heap-object-id-type.md)|堆对象的 ID。|  
|externalObjectAddress|[PROFILER_EXTERNAL_OBJECT_ADDRESS 类型](../../winscript/reference/profiler-external-object-address-type.md)|外部对象的对象地址，例如C++-分配对象，即外部 JavaScript 堆。|  
|typeNameId|[PROFILER_HEAP_OBJECT_NAME_ID 类型](../../winscript/reference/profiler-heap-object-name-id-type.md)|从堆对象类型名称，该 ID 检索[IActiveScriptProfilerHeapEnum::GetNameIdMap](../../winscript/reference/iactivescriptprofilerheapenum-getnameidmap.md)。 只有一个`externalObjectAddress`或`typeName`具体取决于存在`flags`值。|  
|标志|[PROFILER_HEAP_OBJECT_FLAGS 枚举](../../winscript/reference/profiler-heap-object-flags-enumeration.md)|包含有关堆对象的基本信息标志。|  
|optionalInfoCount|USHORT|数[PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)记录可用于堆对象。|