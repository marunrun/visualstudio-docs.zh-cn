---
title: marker_importance 枚举 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::marker_importance
helpviewer_keywords:
- Concurrency::diagnostic::marker_importance enumeration
ms.assetid: d5524ea0-0227-4d8e-9122-332291042df5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b3f5cfb583ec4fceb9fb7428b08c00f6ca8e26b6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62999959"
---
# <a name="markerimportance-enumeration"></a>marker_importance 枚举
表示并发可视化工具标记的重要性级别。

## <a name="syntax"></a>语法

```cpp
enum marker_importance;
```

## <a name="members"></a>成员

### <a name="values"></a>值

|name|说明|
|----------|-----------------|
|`critical_importance`|指定该标记具有关键重要性。|
|`high_importance`|指定该标记具有高重要性。|
|`low_importance`|指定该标记具有低重要性。|
|`normal_importance`|指定该标记具有普通重要性。|

## <a name="requirements"></a>要求
 **标头：** cvmarkersobj.h

 **命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>请参阅
- [diagnostic 命名空间](../profiling/diagnostic-namespace.md)