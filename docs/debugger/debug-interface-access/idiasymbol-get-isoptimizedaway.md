---
title: IDiaSymbol：： get_isOptimizedAway |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: c18b1e38-b152-4a13-aba0-59faded5b2e6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 43ab9598262ba8dd73d6c0725e7bc8450f6ec218
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740155"
---
# <a name="idiasymbolget_isoptimizedaway"></a>IDiaSymbol::get_isOptimizedAway
指定是否对变量进行了优化。

## <a name="syntax"></a>语法

```C++
HRESULT get_isOptimizedAway(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄一个指向 `BOOL` 的指针，该指针指定变量是否已被优化掉。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)