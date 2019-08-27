---
title: IActiveScriptProfilerHeapEnum 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 16756d0e-547a-4825-8b7b-a7e0e4708a04
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fe83f00a96013ffcf7c5df2d47eb1ba7d7a0bae1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992833"
---
# <a name="iactivescriptprofilerheapenum-interface"></a>IActiveScriptProfilerHeapEnum 接口
堆上的迭代器对象与脚本引擎，收集的关联[IActiveScriptProfilerControl3::EnumHeap 方法](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)。  
  
## <a name="syntax"></a>语法  
  
```vb  
interface IActiveScriptProfilerHeapEnum : IUnknown  
```  
  
## <a name="methods"></a>方法  
 [IActiveScriptProfilerHeapEnum::Next 方法](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md)  
 获取下一个或多个对象的堆对象收集的集内[IActiveScriptProfilerControl3::EnumHeap 方法](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)。  
  
 [IActiveScriptProfilerHeapEnum::GetOptionalInfo 方法](../../winscript/reference/iactivescriptprofilerheapenum-getoptionalinfo-method.md)  
 获取指定对象上的可选信息的堆对象收集的集内[IActiveScriptProfilerControl3::EnumHeap 方法](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)。  
  
 [IActiveScriptProfilerHeapEnum::FreeObjectAndOptionalInfo 方法](../../winscript/reference/iactivescriptprofilerheapenum-freeobjectandoptionalinfo-method.md)  
 释放指定[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)结构和与其相关联[PROFILER_HEAP_OBJECT_OPTIONAL_INFO 结构](../../winscript/reference/profiler-heap-object-optional-info-structure.md)元素。  
  
 [IActiveScriptProfilerHeapEnum::GetNameIdMap](../../winscript/reference/iactivescriptprofilerheapenum-getnameidmap.md)  
 返回对应的字符串名称[PROFILER_HEAP_OBJECT_NAME_ID 类型](../../winscript/reference/profiler-heap-object-name-id-type.md)值...