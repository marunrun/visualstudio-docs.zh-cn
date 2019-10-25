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
ms.openlocfilehash: 84dd3e1d107b8e55d5e94979627d1c1586534127
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744492"
---
# <a name="idiaenuminjectedsourcesnext"></a>IDiaEnumInjectedSources::Next
检索枚举序列中指定数量的插入源。

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

中要检索的枚举器中注入的源的数目。

 rgelt

弄返回表示所需注入源的[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)对象的数组。

 pceltFetched

弄返回提取的枚举器中注入的源的数目。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多注入的源，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)