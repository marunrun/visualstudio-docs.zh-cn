---
title: IDiaSymbol：： get_numberOfModifiers |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 61ff7431-1994-4f7e-a182-1817f16f60a9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e034f081f8a279a65134c40e5ee485cd1d08d9b3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739673"
---
# <a name="idiasymbolget_numberofmodifiers"></a>IDiaSymbol::get_numberOfModifiers
检索应用于原始类型的修饰符的数目。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfModifiers(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄一个指向 `DWORD` 的指针，该指针指定应用于原始类型的修饰符的数目。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)