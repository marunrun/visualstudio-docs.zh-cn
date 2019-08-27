---
title: PROFILER_RELATIONSHIP_INFO 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: fae69317-6224-4a6a-8e9e-ccaa6a330818
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0aa0a94668d06f75b959de2ee933ab079feba596
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808888"
---
# <a name="profilerrelationshipinfo-enumeration"></a>PROFILER_RELATIONSHIP_INFO 枚举
表示有关对象关系中的信息。 在中使用[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef [v1_enum] enum {    PROFILER_PROPERTY_TYPE_NUMBER = 0x01,    PROFILER_PROPERTY_TYPE_STRING = 0x02,    PROFILER_PROPERTY_TYPE_HEAP_OBJECT = 0x03,    PROFILER_PROPERTY_TYPE_EXTERNAL_OBJECT = 0x04,    PROFILER_PROPERTY_TYPE_BSTR = 0x05,} PROFILER_RELATIONSHIP_INFO;  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|PROFILER_PROPERTY_TYPE_NUMBER|0x01|该对象是一个数字。|  
|PROFILER_PROPERTY_TYPE_STRING|0x02|该对象是一个字符串。|  
|PROFILER_PROPERTY_TYPE_HEAP_OBJECT|0x03|对象是堆对象。|  
|PROFILER_PROPERTY_TYPE_EXTERNAL_OBJECT|0x04|对象外部，即，不是在垃圾回收堆上。|  
|PROFILER_PROPERTY_TYPE_BSTR|0x05|对象为 BSTR。|  
|PROFILER_PROPERTY_TYPE_SUBSTRING|0x06|对象为子字符串。|