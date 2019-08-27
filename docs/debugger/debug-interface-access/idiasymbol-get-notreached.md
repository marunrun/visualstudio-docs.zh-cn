---
title: 'Idiasymbol:: Get_notreached |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_notReached method
ms.assetid: e44ba922-6cda-40c2-9b62-44e5a8628e63
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5d9882033dd668ef9c907f9b6d466451541225ea
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64784185"
---
# <a name="idiasymbolgetnotreached"></a>IDiaSymbol::get_notReached
检索一个标志，指定是否永远不会达到函数或标签。

## <a name="syntax"></a>语法

```C++
HRESULT get_notReached(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 pFlag

[out]返回`TRUE`永远不会达到的函数或标签; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)