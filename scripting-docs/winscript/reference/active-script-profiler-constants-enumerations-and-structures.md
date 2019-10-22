---
title: 活动脚本探查器常量、枚举和结构 |Microsoft Docs
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
ms.openlocfilehash: 4a9409799c7da2ed3f4864dea0e7785635492220
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572689"
---
# <a name="active-script-profiler-constants-enumerations-and-structures"></a>活动脚本探查器常量、枚举和结构
活动脚本探查器接口使用以下枚举。  
  
## <a name="constants-enumerations-and-structures"></a>常量、枚举和结构  
  
|常量|描述|  
|---------------|-----------------|  
|[PROFILER_EXTERNAL_OBJECT_ADDRESS 类型](../../winscript/reference/profiler-external-object-address-type.md)|探查器的外部对象地址。 用于[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)和[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)。|  
|[PROFILER_HEAP_OBJECT_ID 类型](../../winscript/reference/profiler-heap-object-id-type.md)|堆对象的 ID。 用于[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)[PROFILER_HEAP_OBJECT_SCOPE_LIST 结构](../../winscript/reference/profiler-heap-object-scope-list-structure.md)、 [PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)和[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)。|  
|[PROFILER_HEAP_OBJECT_NAME_ID 类型](../../winscript/reference/profiler-heap-object-name-id-type.md)|堆对象的名称的 ID。 在[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)中使用。|  
  
|枚举|描述|  
|------------------|-----------------|  
|[PROFILER_EVENT_MASK 枚举](../../winscript/reference/profiler-event-mask-enumeration.md)|指示应分析的事件类型。|  
|[PROFILER_HEAP_ENUM_FLAGS 枚举](../../winscript/reference/profiler-heap-enum-flags-enumeration.md)|表示是否公开有关对象关系中指向的堆对象的附加信息的标志。 在[IActiveScriptProfilerControl5：： EnumHeap2 方法](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md)中使用。|  
|[PROFILER_HEAP_OBJECT_FLAGS 枚举](../../winscript/reference/profiler-heap-object-flags-enumeration.md)|表示有关堆对象的基本信息的标志。 在[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)中使用。|  
|[PROFILER_HEAP_OBJECT_OPTIONAL_INFO_TYPE 枚举](../../winscript/reference/profiler-heap-object-optional-info-type-enumeration.md)|表示不同类型的可选信息。 在[PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)中使用。|  
|[PROFILER_RELATIONSHIP_INFO 枚举](../../winscript/reference/profiler-relationship-info-enumeration.md)|表示有关关系中的对象的信息。 在[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)中使用。|  
|[PROFILER_SCRIPT_TYPE 枚举](../../winscript/reference/profiler-script-type-enumeration.md)|指定脚本的类型。|  
  
|结构|描述|  
|----------------|-----------------|  
|[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)|表示由[IActiveScriptProfilerControl3：： EnumHeap 方法](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)收集的堆对象。|  
|[PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)|表示有关堆对象的可选信息。|  
|[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)|表示堆对象的关系。|  
|[PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构](../../winscript/reference/profiler-heap-object-relationship-list-structure.md)|表示属于堆对象的关系的列表。|  
|[PROFILER_HEAP_OBJECT_SCOPE_LIST 结构](../../winscript/reference/profiler-heap-object-scope-list-structure.md)|此结构仅与 function 对象相关联。 作用域列表将函数的闭包表示为一个作用域列表，其中每个作用域都是一个带有关联属性列表（表示每个给定作用域中的变量）的堆对象。 在某些情况下，该范围中的对象的名称可能不可用，只是它们的 id。|  
|[PROFILER_PROPERTY_TYPE_SUBSTRING_INFO 结构](../../winscript/reference/profiler-property-type-substring-info-structure.md)|表示有关子字符串的类型的信息。|  
  
## <a name="see-also"></a>请参阅  
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)