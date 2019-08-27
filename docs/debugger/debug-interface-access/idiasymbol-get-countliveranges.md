---
title: IDiaSymbol::get_countLiveRanges |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_countLiveRanges
ms.assetid: 55f79e1a-d4c2-42cd-ab37-d8253b20e34c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8cd86edee72f3d25763fd3d19dd9c789e152ed6
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62837458"
---
# <a name="idiasymbolgetcountliveranges"></a>IDiaSymbol::get_countLiveRanges
检索有效的地址范围与本地符号数。

## <a name="syntax"></a>语法

```C++
HRESULT get_countLiveRanges ( 
   DWORD* count
);
```

#### <a name="parameters"></a>参数
 `count`

[out]返回地址范围的数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)