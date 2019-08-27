---
title: IDiaSymbol::get_restrictedType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: c48b00a6-26b0-47b0-b824-fe44dedbc756
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8929414c0e36983d378ea2a801803321f3aa88c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62835521"
---
# <a name="idiasymbolgetrestrictedtype"></a>IDiaSymbol::get_restrictedType
指定是否`this`指针被标记为受限。

## <a name="syntax"></a>语法

```C++
HRESULT get_restrictedType(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`BOOL`，它指定是否`this`指针被标记为受限。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)