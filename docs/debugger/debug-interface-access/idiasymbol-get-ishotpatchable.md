---
title: IDiaSymbol：： get_isHotpatchable |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isHotpatchable method
ms.assetid: b7b6f490-1cf2-4a68-9237-b152dac84d3c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27218a2814e14e0a1ec30bd7fb4dc4840589251c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740233"
---
# <a name="idiasymbolget_ishotpatchable"></a>IDiaSymbol::get_isHotpatchable
检索一个标志，该标志指示是否使用[/hotpatch （Create 可热修补 Image）](/cpp/build/reference/hotpatch-create-hotpatchable-image)编译器开关编译该模块。

## <a name="syntax"></a>语法

```C++
HRESULT get_isHotpatchable(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果模块可修补，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 此属性可从 `SymTagCompilandDetails` 符号类型（请参阅[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)）中获取。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)