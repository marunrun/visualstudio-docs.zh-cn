---
title: PROFILER_HEAP_ENUM_FLAGS 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 17936b7a-40d5-4774-b92b-b24ee391591e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d613ed3bcb4699f20d521f08b6c34d55d8363ba4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830352"
---
# <a name="profilerheapenumflags-enumeration"></a>PROFILER_HEAP_ENUM_FLAGS 枚举
表示是否公开有关对象关系中指向的堆对象额外信息的标志。 在中使用[EnumHeap2](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef [v1_enum] enum {    PROFILER_HEAP_ENUM_FLAGS_NONE                      = 0x00000000,    PROFILER_HEAP_ENUM_FLAGS_STORE_RELATIONSHIP_FLAGS  = 0x00000001,} PROFILER_HEAP_ENUM_FLAGS;  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|PROFILER_HEAP_ENUM_FLAGS_NONE|0x00000000|此堆对象不公开有关对象关系的额外信息。 此堆对象的行为方式与[IActiveScriptProfilerControl3::HeapEnum](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)。|  
|PROFILER_HEAP_ENUM_ENUM_ STORE_RELATIONSHIP_FLAGS|0x00000001|此堆对象将公开有关对象关系中指向的对象为 getter 或 setter 方法的信息。 此信息将存储在高 2 个字节 （16 位） 的[PROFILER_HEAP_OBJECT_RELATIONSHIP.relationshipInfo](../../winscript/reference/profiler-heap-object-relationship-structure.md)字段作为之一[PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS](../../winscript/reference/profiler-heap-object-relationship-flags-enumeration.md)枚举值。|  
|PROFILER_HEAP_ENUM_FLAGS_SUBSTRINGS|0x00000002|此堆对象用于正确显示子字符串。|  
|PROFILER_HEAP_ENUM_FLAGS_RELATIONSHIP_SUBSTRINGS|PROFILER_HEAP_ENUM_FLAGS_STORE_RELATIONSHIP_FLAGS &#124; PROFILER_HEAP_ENUM_FLAGS_SUBSTRINGS|此堆对象用于正确显示子字符串。|