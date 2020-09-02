---
title: marker_importance 枚举 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::marker_importance
helpviewer_keywords:
- Concurrency::diagnostic::marker_importance enumeration
ms.assetid: d5524ea0-0227-4d8e-9122-332291042df5
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a4451a7b222b66f0fe5bea2b0e5f2b8499c9033c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198380"
---
# <a name="marker_importance-enumeration"></a>marker_importance 枚举
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

表示并发可视化工具标记的重要性级别。  
  
## <a name="syntax"></a>语法  
  
```  
enum marker_importance;  
```  
  
## <a name="members"></a>成员  
  
### <a name="values"></a>值  
  
|“属性”|描述|  
|----------|-----------------|  
|`critical_importance`|指定该标记具有关键重要性。|  
|`high_importance`|指定该标记具有高重要性。|  
|`low_importance`|指定该标记具有低重要性。|  
|`normal_importance`|指定该标记具有普通重要性。|  
  
## <a name="requirements"></a>要求  
 **标头：** cvmarkersobj.h  
  
 **命名空间：** Concurrency::diagnostic  
  
## <a name="see-also"></a>另请参阅  
 [诊断命名空间](../profiling/diagnostic-namespace.md)
