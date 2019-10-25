---
title: IDiaSymbol：： get_numberOfRegisterIndices |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 1ec8b8ea-e423-4327-8dc0-a390e6e3ffb0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6074f8d4954ced530640bedcd60ab397a2840e98
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739659"
---
# <a name="idiasymbolget_numberofregisterindices"></a>IDiaSymbol::get_numberOfRegisterIndices
检索寄存器索引的数目。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfRegisterIndices(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄一个指针，指向包含寄存器索引数的 `DWORD`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)