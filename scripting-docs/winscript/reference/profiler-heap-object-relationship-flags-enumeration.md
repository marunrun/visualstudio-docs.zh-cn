---
title: PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1a41b642-c9a9-4d83-b943-d59b232eebf6
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 322f6f3352c1b0dfad4572d55e1ebe2388c8cc4a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823629"
---
# <a name="profilerheapobjectrelationshipflags-enumeration"></a>PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS 枚举
标志表示对象关系中指向的堆对象是否为 getter 或 setter 方法。 在中使用[EnumHeap2](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md)方法中指定了 PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS 值时`enumFlags`参数。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef [v1_enum] enum {    PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_NONE                      = 0x00000000,    PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_GET_ACCESSOR           = 0x00010000,    PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_SET_ACCESSOR           = 0x00020000,} PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS;  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_NONE|0x00000000|对象关系中指向此堆对象不被标识为 getter 或 setter 方法。|  
|PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_GET_ACCESSOR|0x00010000|对象关系中指向的堆对象是 getter 方法。 此信息将存储在高 2 个字节 （16 位） 的[PROFILER_HEAP_OBJECT_RELATIONSHIP.relationshipInfo](../../winscript/reference/profiler-heap-object-relationship-structure.md)字段。|  
|PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_SET_ACCESSOR|0x00020000|对象关系中指向的堆对象是 setter 方法。 此信息将存储在高 2 个字节 （16 位） 的`PROFILER_HEAP_OBJECT_RELATIONSHIP.relationshipInfo`字段。|