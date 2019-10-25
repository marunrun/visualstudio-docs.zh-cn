---
title: IDiaSymbol：： get_InlSpec |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_InlSpec method
ms.assetid: 30af6a2f-be84-429e-a96a-d0f9ed9343fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5675239e35ab3bef809e3d54544d87d7a9e8bb75
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740385"
---
# <a name="idiasymbolget_inlspec"></a>IDiaSymbol::get_InlSpec
此函数检索一个标志，该标志指示是否将函数标记为内联（使用[内联、__inline、\__forceinline](/cpp/cpp/inline-functions-cpp)属性之一）。

## <a name="syntax"></a>语法

```C++
HRESULT get_inlSpec(
   BOOL *pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果函数标记为内联，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [inline、__inline、\__forceinline](/cpp/cpp/inline-functions-cpp)