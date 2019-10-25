---
title: IDiaSymbol：： get_framePointerPresent |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePointerPresent method
ms.assetid: d036090a-1651-454d-9130-b798f58ba053
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1fce085f134b844d7e53e19d9e2ec057aa8a89ca
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740671"
---
# <a name="idiasymbolget_framepointerpresent"></a>IDiaSymbol::get_framePointerPresent
检索一个标志，该标志指定是否存在帧指针。 当[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)设置为 `SymTagFunction` 时使用。

## <a name="syntax"></a>语法

```C++
HRESULT get_framePointerPresent( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]]如果存在帧指针，则返回 `TRUE`;否则，将返回 `FALSE`。

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