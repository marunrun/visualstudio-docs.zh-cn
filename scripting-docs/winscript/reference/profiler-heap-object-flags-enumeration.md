---
title: PROFILER_HEAP_OBJECT_FLAGS 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0f517743-cc4a-4911-add3-a43680071a1f
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f7fde5ed275691d78e534cd7b8d8e958a8f20325
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823832"
---
# <a name="profilerheapobjectflags-enumeration"></a>PROFILER_HEAP_OBJECT_FLAGS 枚举
表示堆对象有关的基本信息的标志。 在中使用[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef [v1_enum] enum {    PROFILER_HEAP_OBJECT_FLAGS_NEW_OBJECT            = 0x00000001,    PROFILER_HEAP_OBJECT_FLAGS_IS_ROOT               = 0x00000002,    PROFILER_HEAP_OBJECT_FLAGS_SITE_CLOSED           = 0x00000004,    PROFILER_HEAP_OBJECT_FLAGS_EXTERNAL              = 0x00000008,    PROFILER_HEAP_OBJECT_FLAGS_EXTERNAL_UNKNOWN      = 0x00000010,    PROFILER_HEAP_OBJECT_FLAGS_EXTERNAL_DISPATCH     = 0x00000020,    PROFILER_HEAP_OBJECT_FLAGS_SIZE_APPROXIMATE      = 0x00000040,    PROFILER_HEAP_OBJECT_FLAGS_SIZE_UNAVAILABLE      = 0x00000080,    PROFILER_HEAP_OBJECT_FLAGS_NEW_STATE_UNAVAILABLE = 0x00000100,    PROFILER_HEAP_OBJECT_FLAGS_WINRT_INSTANCE        = 0x00000200,    PROFILER_HEAP_OBJECT_FLAGS_WINRT_RUNTIMECLASS    = 0x00000400,    PROFILER_HEAP_OBJECT_FLAGS_WINRT_DELEGATE        = 0x00000800,    PROFILER_HEAP_OBJECT_FLAGS_WINRT_NAMESPACE       = 0x00001000,} PROFILER_HEAP_OBJECT_FLAGS;  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|PROFILER_HEAP_OBJECT_FLAGS_NEW_OBJECT|0x00000001|此堆对象所分配的上一堆枚举请求之后。 [PROFILER_HEAP_OBJECT_ID 类型](../../winscript/reference/profiler-heap-object-id-type.md)可以重复使用的值，如果对象被收集。|  
|PROFILER_HEAP_OBJECT_FLAGS_IS_ROOT|0x00000002|此堆对象是对象图的根对象。|  
|PROFILER_HEAP_OBJECT_FLAGS_SITE_CLOSED|0x00000004|此堆对象是从已关闭的脚本站点。|  
|PROFILER_HEAP_OBJECT_FLAGS_EXTERNAL|0x00000008|此堆对象外部 JavaScript 垃圾回收堆分配。|  
|PROFILER_HEAP_OBJECT_FLAGS_EXTERNAL_UNKNOWN|0x00000010|此堆对象所分配的垃圾回收堆和实现 IUnknown 之外。|  
|PROFILER_HEAP_OBJECT_FLAGS_EXTERNAL_DISPATCH|0x00000020|此堆对象被垃圾回收堆之外分配，并实现 IDISPATCH 接口。|  
|PROFILER_HEAP_OBJECT_FLAGS_SIZE_APPROXIMATE|0x00000040|此堆对象的大小为近似大小。|  
|PROFILER_HEAP_OBJECT_FLAGS_SIZE_UNAVAILABLE|x00000080|此堆对象的大小将不可用。|  
|PROFILER_HEAP_OBJECT_FLAGS_WINRT_INSTANCE|0x00000200|堆对象是 Windows 运行时实例。|  
|PROFILER_HEAP_OBJECT_FLAGS_WINRT_RUNTIMECLASS|0x00000400|堆对象是一个 Windows 运行时运行时类。|  
|PROFILER_HEAP_OBJECT_FLAGS_WINRT_DELEGATE|0x00000800|堆对象是一个 Windows 运行时委托。|  
|PROFILER_HEAP_OBJECT_FLAGS_WINRT_NAMESPACE|0x00001000|堆对象是 Windows 运行时命名空间中。|