---
title: PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 77e638bd-ae36-4292-a170-90a0c500e610
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4c7f28499b5d6e1e01caab1e6fd83fc5ab72ccf6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823861"
---
# <a name="profilerheapobjectoptionalinfo-structure"></a>PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构
表示堆对象的可选信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct _PROFILER_HEAP_OBJECT_OPTIONAL_INFO{    PROFILER_HEAP_OBJECT_OPTIONAL_INFO_TYPE infoType;    [switch_type(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_TYPE), switch_is(infoType)] union    {        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_PROTOTYPE)] PROFILER_HEAP_OBJECT_ID prototype;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_FUNCTION_NAME)] LPCWSTR functionName;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_ELEMENT_ATTRIBUTES_SIZE)] UINT elementAttributesSize;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_ELEMENT_TEXT_CHILDREN_SIZE)] UINT elementTextChildrenSize;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_SCOPE_LIST)] PROFILER_HEAP_OBJECT_SCOPE_LIST* scopeList;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_INTERNAL_PROPERTY)] PROFILER_HEAP_OBJECT_RELATIONSHIP* internalProperty;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_NAME_PROPERTIES)] PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST* namePropertyList;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_INDEX_PROPERTIES)] PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST* indexPropertyList;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_RELATIONSHIPS)] PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST* relationshipList;        [case(PROFILER_HEAP_OBJECT_OPTIONAL_INFO_WINRTEVENTS)] PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST* eventList;    };} PROFILER_HEAP_OBJECT_OPTIONAL_INFO;  
```  
  
## <a name="members"></a>成员  
  
|成员|类型|描述|  
|------------|----------|-----------------|  
|infoType|[PROFILER_HEAP_OBJECT_OPTIONAL_INFO_TYPE 枚举](../../winscript/reference/profiler-heap-object-optional-info-type-enumeration.md)|可选信息的类型。|  
|原型|[PROFILER_HEAP_OBJECT_ID 类型](../../winscript/reference/profiler-heap-object-id-type.md)|堆对象的原型对象的 ID。|  
|functionName|LPCWSTR|堆对象的函数名称。|  
|elementAttributesSize|UINT|堆对象的元素属性的大小。|  
|elementTextChildrenSize|UINT|堆对象的文本子项的大小。|  
|scopeList|[PROFILER_HEAP_OBJECT_SCOPE_LIST 结构](../../winscript/reference/profiler-heap-object-scope-list-structure.md)|堆对象的作用域列表。|  
|internalProperty|[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)|堆对象的内部属性。|  
|namePropertyList|[PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构](../../winscript/reference/profiler-heap-object-relationship-list-structure.md)|堆对象的名称属性的列表。|  
|indexPropertyList|[PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构](../../winscript/reference/profiler-heap-object-relationship-list-structure.md)|堆对象的索引属性的列表。|  
|relationshipList|[PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构](../../winscript/reference/profiler-heap-object-relationship-list-structure.md)|堆对象的关系的列表。|  
|eventList|[PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构](../../winscript/reference/profiler-heap-object-relationship-list-structure.md)|堆对象的事件的列表。|