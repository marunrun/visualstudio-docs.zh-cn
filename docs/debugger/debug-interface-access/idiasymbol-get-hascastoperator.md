---
title: IDiaSymbol：： get_hasCastOperator |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasCastOperator method
ms.assetid: a21114a6-56a3-4e8a-a65f-58ec2a0a8908
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5a5d030e56a279615dd2f23785993a0386a7380d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740566"
---
# <a name="idiasymbolget_hascastoperator"></a>IDiaSymbol::get_hasCastOperator
检索一个标志，该标志指定用户定义数据类型是否已定义任何强制转换运算符。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasCastOperator ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果用户定义数据类型定义了任何转换运算符，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)