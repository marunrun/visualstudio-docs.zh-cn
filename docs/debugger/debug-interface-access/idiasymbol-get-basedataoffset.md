---
title: IDiaSymbol：： get_baseDataOffset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: bb2ff5ed-9293-4c37-9741-654058b571c5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 298903e4e76c34fe1013b0f26729fb900c7b3fea
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740986"
---
# <a name="idiasymbolget_basedataoffset"></a>IDiaSymbol::get_baseDataOffset
检索基本数据偏移量。

## <a name="syntax"></a>语法

```C++
HRESULT get_baseDataOffset(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄指向保存基本数据偏移量的 `DWORD` 的指针。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)