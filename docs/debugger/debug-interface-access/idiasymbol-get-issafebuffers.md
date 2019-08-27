---
title: 'Idiasymbol:: Get_issafebuffers |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isSafeBuffers method
ms.assetid: f29e373d-e7bb-4181-ab9f-bf708d401d83
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f5dd923b9f7244bb42fdf8defb70b8ed5dc82ed0
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64825503"
---
# <a name="idiasymbolgetissafebuffers"></a>IDiaSymbol::get_isSafeBuffers
检索用于指定是否使用安全的缓冲区的预处理器指令的标志。 何时使用[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)设置为`SymTagFunction`。

## <a name="syntax"></a>语法

```C++
HRESULT get_isSafeBuffers( 
   BOOL* pRetVal)
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果指针使用预处理器指令的安全缓冲区中; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [strict_gs_check](/cpp/preprocessor/strict-gs-check)