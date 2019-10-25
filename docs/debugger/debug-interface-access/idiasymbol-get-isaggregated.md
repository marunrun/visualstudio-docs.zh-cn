---
title: IDiaSymbol：： get_isAggregated |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isAggregated method
ms.assetid: 24d280ef-6ea3-4958-9418-4ad3ca7c67c1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee36d1901f7acb5bc7e41ac72b8dc03b15bc45c8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740300"
---
# <a name="idiasymbolget_isaggregated"></a>IDiaSymbol::get_isAggregated
检索一个标志，该标志指定该数据符号是否为聚合或符号集合的一部分;编译器会将聚合符号视为单独的实体，但它们实际上是一个大符号的组成部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAggregated(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果数据是从父符号拆分的符号聚合的一部分，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 对于作为聚合符号父级的符号， [IDiaSymbol：： get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)方法是 `TRUE` 的。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)