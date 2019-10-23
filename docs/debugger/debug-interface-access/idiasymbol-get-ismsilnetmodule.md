---
title: IDiaSymbol::get_isMSILNetmodule | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isMSILNetmodule method
ms.assetid: 593827f3-8437-4a12-ada4-ff715ec95fb2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 322a4ef059c190e3ba73bbce6f80978530270ece
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740190"
---
# <a name="idiasymbolget_ismsilnetmodule"></a>IDiaSymbol::get_isMSILNetmodule
检索一个标志，该标志指示该模块是否为 .netmodule （仅包含元数据的 Microsoft 中间语言（MSIL）模块，而不包含本机符号）。

## <a name="syntax"></a>语法

```C++
HRESULT get_isMSILNetmodule(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果模块为 MSIL，则返回 `TRUE`;否则，将返回 `FALSE`。

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