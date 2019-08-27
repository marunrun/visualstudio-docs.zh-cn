---
title: IDiaEnumInjectedSources::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources::Next method
ms.assetid: 38af80fc-748f-4b15-bff1-823db21dd4d0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aea793f33eb78ee1637d7f22eb46ba34514e0e8f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554028"
---
# <a name="idiaenuminjectedsourcesnext"></a>IDiaEnumInjectedSources::Next
检索指定的数目的枚举序列中的插入源。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG                celt,
   IDiaInjectedSource** rgelt,
   ULONG*               pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in]要检索的枚举器中的插入源数。

 rgelt

[out]返回的数组[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)对象，表示所需的插入的源。

 pceltFetched

[out]返回多个插入的源中提取枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多插入的源。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)