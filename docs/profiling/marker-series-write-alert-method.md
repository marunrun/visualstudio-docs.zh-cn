---
title: marker_series::write_alert 方法 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic:marker_series::write_alert
helpviewer_keywords:
- Concurrency, diagnostic:marker_series::write_alert method
ms.assetid: 9d5465c7-f862-47a7-b249-4116605075a6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d5e79bab25885c8759ea5726b037771a4943c563
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85329631"
---
# <a name="marker_serieswrite_alert-method"></a>marker_series::write_alert 方法
向并发可视化工具跟踪文件写入一个警报。

## <a name="syntax"></a>语法

```cpp
void write_alert(
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>参数
 `_Format` 一个复合格式字符串，其中包含与零个或多个格式项混合的文本，这些格式项对应于参数列表中的对象。

## <a name="requirements"></a>要求
 **Header:** *cvmarkersobj.h*

 **命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>请参阅
- [marker_series 类](../profiling/marker-series-class.md)