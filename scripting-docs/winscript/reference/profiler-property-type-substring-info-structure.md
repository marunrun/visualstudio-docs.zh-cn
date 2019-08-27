---
title: PROFILER_PROPERTY_TYPE_SUBSTRING_INFO 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3845c872-4302-47b6-8912-7b2d7a3b3357
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 5f873cdf2ebd394e48c1513135f1acdcd700c283
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62816891"
---
# <a name="profilerpropertytypesubstringinfo-structure"></a>PROFILER_PROPERTY_TYPE_SUBSTRING_INFO 结构
表示有关在关系中使用的子字符串类型的信息。 在中使用[PROFILER_HEAP_OBJECT_RELATIONSHIP 结构](../../winscript/reference/profiler-heap-object-relationship-structure.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct _PROFILER_PROPERTY_TYPE_SUBSTRING_INFO {    UINT length;    LPCWSTR value; } PROFILER_PROPERTY_TYPE_SUBSTRING_INFO;  
```  
  
## <a name="members"></a>成员  
  
|成员|类型|描述|  
|------------|----------|-----------------|  
|length|UINT|对象为 UINT。|  
|值|LPCWSTR|对象为 LPCWSTR。|