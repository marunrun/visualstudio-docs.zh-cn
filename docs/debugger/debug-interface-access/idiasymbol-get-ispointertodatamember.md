---
title: IDiaSymbol：： get_isPointerToDataMember |Microsoft Docs
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
ms.openlocfilehash: 2e06a8605b38042773cfa60e4847ed3ace9c5954
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740128"
---
# <a name="idiasymbolget_ispointertodatamember"></a>IDiaSymbol::get_isPointerToDataMember
指定此符号是否为指向数据成员的指针。

## <a name="syntax"></a>语法

```C++
HRESULT get_isPointerToDataMember(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄一个指向 `BOOL` 的指针，该指针指定此符号是否为指向数据成员的指针。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)