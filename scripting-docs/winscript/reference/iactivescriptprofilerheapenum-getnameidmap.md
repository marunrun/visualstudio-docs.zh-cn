---
title: IActiveScriptProfilerHeapEnum::GetNameIdMap | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 88514c93-850b-48d4-9a68-1e27d7411f0d
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3284557bf71a038d884c1f8786755b7761770e21
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992853"
---
# <a name="iactivescriptprofilerheapenumgetnameidmap"></a>IActiveScriptProfilerHeapEnum::GetNameIdMap
返回对应的字符串名称[PROFILER_HEAP_OBJECT_NAME_ID 类型](../../winscript/reference/profiler-heap-object-name-id-type.md)值。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetNameIdMap (    [out, size_is(,*pcelt)] LPCWSTR* pNameList[],     [out] UINT *pcelt);  
```  
  
#### <a name="parameters"></a>参数  
 `pNameList`  
 [out]与关联的名称数组[PROFILER_HEAP_OBJECT_NAME_ID 类型](../../winscript/reference/profiler-heap-object-name-id-type.md)值。  
  
 `pcelt`  
 [out]数组中的名称数。  
  
## <a name="return-value"></a>返回值  
 HRESULT。