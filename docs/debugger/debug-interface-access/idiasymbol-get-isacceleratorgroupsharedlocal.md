---
title: IDiaSymbol::get_isAcceleratorGroupSharedLocal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 17a20542-5b45-478f-bb80-0d56031aadb5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d6cf755121f851e652cce251ace2105e6773822
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740335"
---
# <a name="idiasymbolget_isacceleratorgroupsharedlocal"></a>IDiaSymbol::get_isAcceleratorGroupSharedLocal
检索一个标志，该标志指示符号是否与为C++ AMP 加速器编译的代码中的组共享本地变量相对应。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAcceleratorGroupSharedLocal(
   BOOL* pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄一个指向 `BOOL` 的指针，该指针指示符号是否与为C++ AMP 加速器编译的代码中的组共享本地变量相对应。 如果 `TRUE`，则可以使用 `get_baseDataSlot` 和 `get_baseDataOffset` 方法来获取变量的存储位置信息。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)
- [IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)