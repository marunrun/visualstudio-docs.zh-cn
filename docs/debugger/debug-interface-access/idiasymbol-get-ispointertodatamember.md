---
title: IDiaSymbol::get_isPointerToDataMember |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: ef17c737-242e-43e8-b7e1-2c3bc58cfcef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d74c2ba8317098212c7263ab049becc52f874e9
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62836575"
---
# <a name="idiasymbolgetispointertodatamember"></a>IDiaSymbol::get_isPointerToDataMember
指定此符号是否为指向数据成员的指针。

## <a name="syntax"></a>语法

```C++
HRESULT get_isPointerToDataMember(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`BOOL`，指定此符号是否为指向数据成员的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)