---
title: PROFILER_HEAP_OBJECT_SCOPE_LIST 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 33ebaa31-0a35-47d5-a4e3-afd83e16f53e
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b1285e4efa3db8a7ec99808f5888d3dbf948e589
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830316"
---
# <a name="profilerheapobjectscopelist-structure"></a>PROFILER_HEAP_OBJECT_SCOPE_LIST 结构
此结构是函数对象仅与相关联。 作用域列表表示为其中每个作用域是一个具有表示每个给定范围中的变量的关联的属性列表的堆对象的作用域的列表，该函数的闭包。 在某些情况下，作用域可能不可用中的对象和仅其索引的属性列表的名称是可用。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct _PROFILER_HEAP_OBJECT_SCOPE_LIST{    UINT count;    [size_is(count)] PROFILER_HEAP_OBJECT_ID scopes[];} PROFILER_HEAP_OBJECT_SCOPE_LIST;  
```  
  
## <a name="members"></a>成员  
  
|成员|类型|描述|  
|------------|----------|-----------------|  
|count|UINT|作用域的数量|  
|scopes|[PROFILER_HEAP_OBJECT_ID 类型](../../winscript/reference/profiler-heap-object-id-type.md)|范围的数组。|