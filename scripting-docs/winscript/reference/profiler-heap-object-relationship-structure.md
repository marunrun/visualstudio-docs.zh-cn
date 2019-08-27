---
title: PROFILER_HEAP_OBJECT_RELATIONSHIP 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3ab3d986-3314-4c7b-a1c8-18ed691a8b9c
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7a905a44f2ef686181c5a859699277d16f6cd374
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823616"
---
# <a name="profilerheapobjectrelationship-structure"></a>PROFILER_HEAP_OBJECT_RELATIONSHIP 结构
表示堆对象的关系。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct _PROFILER_HEAP_OBJECT_RELATIONSHIP{    PROFILER_HEAP_OBJECT_NAME_ID relationshipId;    PROFILER_RELATIONSHIP_INFO relationshipInfo;    [switch_type(PROFILER_RELATIONSHIP_INFO), switch_is(relationshipInfo)] union    {        [case(PROFILER_PROPERTY_TYPE_NUMBER)] double numberValue;        [case(PROFILER_PROPERTY_TYPE_STRING)] LPCWSTR stringValue;        [case(PROFILER_PROPERTY_TYPE_HEAP_OBJECT)] PROFILER_HEAP_OBJECT_ID objectId;        [case(PROFILER_PROPERTY_TYPE_EXTERNAL_OBJECT)] PROFILER_EXTERNAL_OBJECT_ADDRESS externalObjectAddress;    };} PROFILER_HEAP_OBJECT_RELATIONSHIP;  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|relationshipId|[PROFILER_HEAP_OBJECT_NAME_ID 类型](../../winscript/reference/profiler-heap-object-name-id-type.md)|Relationship 的 ID 名称，从[IActiveScriptProfilerHeapEnum::GetNameIdMap](../../winscript/reference/iactivescriptprofilerheapenum-getnameidmap.md)。|  
|relationshipInfo|[PROFILER_RELATIONSHIP_INFO 枚举](../../winscript/reference/profiler-relationship-info-enumeration.md)|有关关系的信息。|  
|numberValue|double|数字值。 只有一个`numberValue` / `stringValue` / `objectId` / `externalObjectAddress`设置，基于`relationshipInfo`值。|  
|stringValue|LPCWSTR|字符串值。|  
|objectId|[PROFILER_HEAP_OBJECT_ID 类型](../../winscript/reference/profiler-heap-object-id-type.md)|堆对象的 ID。|  
|externalObjectAddress|[PROFILER_EXTERNAL_OBJECT_ADDRESS 类型](../../winscript/reference/profiler-external-object-address-type.md)|外部对象地址中。|  
|subString|[PROFILER_PROPERTY_TYPE_SUBSTRING_INFO 结构](../../winscript/reference/profiler-property-type-substring-info-structure.md)|有关子字符串类型的信息。|