---
title: 'Iactivescriptprofilerheapenum:: Next 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0336286f-1dcd-4df9-adf5-76b59b4e74bb
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4bad607db168d5f3e3533087c94c6c0970f5eb24
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992822"
---
# <a name="iactivescriptprofilerheapenumnext-method"></a>IActiveScriptProfilerHeapEnum::Next 方法
获取下一个对象中的一堆对象从[IActiveScriptProfilerControl3::EnumHeap 方法](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Next (    [in] ULONG celt,    [out, size_is(celt), length_is(*pceltFetched)] PROFILER_HEAP_OBJECT** heapObjects,     [out] ULONG *pceltFetched);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 要返回的对象数。  
  
 `heapObjects`  
 [out]下一步[PROFILER_HEAP_OBJECT 结构](../../winscript/reference/profiler-heap-object-structure.md)结构。  
  
 `pceltFetched`  
 [out]返回的对象数  
  
## <a name="return-value"></a>返回值  
 HRESULT。