---
title: IDiaSymbol：： get_isSplitted |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isSplitted method
ms.assetid: ff160cf6-003b-4ef5-a406-20a7b287b2bf
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9511551a2f3530adc14bee0f6eec3cf360b41c03
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740043"
---
# <a name="idiasymbolget_issplitted"></a>IDiaSymbol::get_isSplitted
检索一个标志，该标志指定数据符号是否已拆分为聚合或其他符号的集合。编译器会将符号视为单独的实体，即使它们确实是较大符号的组成部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_isSplitted(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果符号已拆分为符号聚合，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 [IDiaSymbol：： get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)方法为作为拆分符号一部分的所有符号返回 `TRUE`。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)