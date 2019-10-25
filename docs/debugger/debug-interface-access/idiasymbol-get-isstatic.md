---
title: IDiaSymbol：： get_isStatic |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isStatic method
ms.assetid: 3be5fe1b-46e8-4b07-90d8-4929dbbe7ff7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 498786935ceb71c9d271487630317057e2adbb9f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740039"
---
# <a name="idiasymbolget_isstatic"></a>IDiaSymbol::get_isStatic
检索一个标志，该标志指定是否已将函数或 thunk 层标记为静态。

## <a name="syntax"></a>语法

```C++
HRESULT get_isStatic(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果函数或 thunk 层已标记为静态，则返回 `TRUE`;否则，将返回 `FALSE`。

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