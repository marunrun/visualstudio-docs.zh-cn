---
title: IDiaSymbol::get_isPointerToMemberFunction |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: aa9b5599-9602-41be-ab50-d84b90bee72f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b666aa19e574702655178790b8aa0463a0d5c2d5
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62836541"
---
# <a name="idiasymbolgetispointertomemberfunction"></a>IDiaSymbol::get_isPointerToMemberFunction
指定此符号是否为指向成员函数的指针。

## <a name="syntax"></a>语法

```C++
HRESULT get_isPointerToMemberFunction(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`BOOL`，指定此符号是否为指向成员函数的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)