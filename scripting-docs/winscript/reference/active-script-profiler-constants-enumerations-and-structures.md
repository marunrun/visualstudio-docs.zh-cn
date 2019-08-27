---
title: 活动脚本 Profiler 常量、 枚举和结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6e079d84-9dde-46fc-8a6a-18e902f60ecc
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1d39e6feb2cddd0c573368db9bf50b1e77f2e48d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955490"
---
# <a name="active-script-profiler-constants-enumerations-and-structures"></a>活动脚本探查器常量、枚举和结构
活动脚本 Profiler 接口使用以下枚举。  
  
## <a name="constants-enumerations-and-structures"></a>常量、枚举和结构  
  
|常量|描述|  
|---------------|-----------------|  
|[PROFILER_EXTERNAL_OBJECT_ADDRESS 类型](../../winscript/reference/profiler-external-object-address-type.md)|探查器的外部对象地址。 在中使用[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)并[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)。|  
|[PROFILER_HEAP_OBJECT_ID 类型](../../winscript/reference/profiler-heap-object-id-type.md)|堆对象的 ID。 在中使用[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)[PROFILER_HEAP_OBJECT_SCOPE_LIST 结构](../../winscript/reference/profiler-heap-object-scope-list-structure.md)， [PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)，以及[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)。|  
|[PROFILER_HEAP_OBJECT_NAME_ID 类型](../../winscript/reference/profiler-heap-object-name-id-type.md)|堆对象的名称的 ID。 在中使用[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)。|  
  
|枚举|描述|  
|------------------|-----------------|  
|[PROFILER_EVENT_MASK 枚举](../../winscript/reference/profiler-event-mask-enumeration.md)|指示应进行事件探查的事件的类型。|  
|[PROFILER_HEAP_ENUM_FLAGS 枚举](../../winscript/reference/profiler-heap-enum-flags-enumeration.md)|表示是否公开有关对象关系中指向的堆对象额外信息的标志。 在中使用[IActiveScriptProfilerControl5::EnumHeap2 方法](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md)。|  
|[PROFILER_HEAP_OBJECT_FLAGS 枚举](../../winscript/reference/profiler-heap-object-flags-enumeration.md)|表示堆对象有关的基本信息的标志。 在中使用[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)。|  
|[PROFILER_HEAP_OBJECT_OPTIONAL_INFO_TYPE 枚举](../../winscript/reference/profiler-heap-object-optional-info-type-enumeration.md)|表示不同类型的可选信息。 在中使用[PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)。|  
|[PROFILER_RELATIONSHIP_INFO 枚举](../../winscript/reference/profiler-relationship-info-enumeration.md)|表示有关对象关系中的信息。 在中使用[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)。|  
|[PROFILER_SCRIPT_TYPE 枚举](../../winscript/reference/profiler-script-type-enumeration.md)|指定脚本的类型。|  
  
|结构|描述|  
|----------------|-----------------|  
|[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)|表示堆对象收集[IActiveScriptProfilerControl3::EnumHeap 方法](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)。|  
|[PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)|表示堆对象的可选信息。|  
|[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)|表示堆对象的关系。|  
|[PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构](../../winscript/reference/profiler-heap-object-relationship-list-structure.md)|表示属于堆对象的关系的列表。|  
|[PROFILER_HEAP_OBJECT_SCOPE_LIST 结构](../../winscript/reference/profiler-heap-object-scope-list-structure.md)|此结构是函数对象仅与相关联。 作用域列表表示为其中每个作用域是一个具有表示每个给定范围中的变量的关联的属性列表的堆对象的作用域的列表，该函数的闭包。 在某些情况下，可能不可用，该作用域中的对象名称只有及其 id。|  
|[PROFILER_PROPERTY_TYPE_SUBSTRING_INFO 结构](../../winscript/reference/profiler-property-type-substring-info-structure.md)|表示有关的子字符串的类型的信息。|  
  
## <a name="see-also"></a>请参阅  
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)