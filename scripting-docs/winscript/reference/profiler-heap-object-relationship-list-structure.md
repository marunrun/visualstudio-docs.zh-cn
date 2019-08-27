---
title: PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 46ca87ea-5b0f-437d-a33f-b2d9a457e036
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 23c6ee5f8ff4d7a8a19c19bae55bb72eb5c8fd06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823874"
---
# <a name="profilerheapobjectrelationshiplist-structure"></a>PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST 结构
表示属于堆对象的关系的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct _PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST{    UINT count;    [size_is(count)] PROFILER_HEAP_OBJECT_RELATIONSHIP elements[];} PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST;  
```  
  
## <a name="members"></a>成员  
  
|成员|类型|描述|  
|------------|----------|-----------------|  
|count|UINT|关系的堆对象数。|  
|元素|[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)|堆对象的关系。|