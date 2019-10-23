---
title: IDiaSymbol：： get_isSafeBuffers |Microsoft Docs
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
ms.openlocfilehash: 0f4c3ab653c0a5540410d8e3e0b5426c4d0bcde5
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740092"
---
# <a name="idiasymbolget_issafebuffers"></a>IDiaSymbol::get_isSafeBuffers
检索一个标志，该标志指定是否使用安全缓冲区的 preprocesser 指令。 当[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)设置为 `SymTagFunction` 时使用。

## <a name="syntax"></a>语法

```C++
HRESULT get_isSafeBuffers( 
   BOOL* pRetVal)
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果指针为安全缓冲区使用预处理器指令，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [strict_gs_check](/cpp/preprocessor/strict-gs-check)