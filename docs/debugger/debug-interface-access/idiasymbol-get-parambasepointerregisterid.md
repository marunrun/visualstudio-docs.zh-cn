---
title: IDiaSymbol::get_paramBasePointerRegisterId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_paramBasePointerRegisterId method
ms.assetid: 9f5caeb4-5c88-4054-bf8b-50d34bbbf8c5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 09bdfb5d276e4dc7414c78529c2a6f1644597cd3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739517"
---
# <a name="idiasymbolget_parambasepointerregisterid"></a>IDiaSymbol::get_paramBasePointerRegisterId
检索包含指向参数的基指针的寄存器 ID。 当[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)设置为 `SymTagFunction` 时使用。

## <a name="syntax"></a>语法

```C++
HRESULT get_paramBasePointerRegisterId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回寄存器的 ID，该 ID 包含指向参数的基指针。

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