---
title: 'marker_series:: write_message 方法 | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::marker_series::write_message
helpviewer_keywords:
- Concurrency::diagnostic::marker_series::write_message method
ms.assetid: 546121bc-67e0-4a5a-a456-12bd78fd6de2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: be6194936264d6038c4dc1e26b5d05f539f0dc6a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62830897"
---
# <a name="marker_serieswrite_message-method"></a>marker_series::write_message 方法
向并发可视化工具跟踪文件写入一条消息。

## <a name="syntax"></a>语法

```cpp
void write_message(
   _In_ LPCTSTR _Format,
   ...
);
void write_message(
   marker_importance _Importance,
   _In_ LPCTSTR _Format,
   ...
);
void write_message(
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
void write_message(
   marker_importance _Importance,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>参数
 `_Format` 一个复合格式字符串，其中包含与零个或多个格式项混合的文本，这些格式项对应于参数列表中的对象。

 `_Importance` 重要性级别。

 `_Category` Category.Importance 级别。

## <a name="requirements"></a>要求
 **Header:** *cvmarkersobj.h*

 **命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>请参阅
- [marker_series 类](../profiling/marker-series-class.md)