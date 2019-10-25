---
title: IDiaSymbol::get_unmodifiedType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_unmodifiedType method
ms.assetid: bf914dc0-ff84-4f5d-9f75-1733b17f3be0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 47841f5fe4abeafe7c522784db337b1960081439
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738986"
---
# <a name="idiasymbolget_unmodifiedtype"></a>IDiaSymbol::get_unmodifiedType
检索此符号的原始类型。 当[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)设置为类型时，请使用。

## <a name="syntax"></a>语法

```C++
HRESULT get_unmodifiedType( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，该对象表示此符号的原始类型。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 当前类型是对返回的原始类型的修改。 通过首先获取符号类型，然后询问返回类型作为原始类型，可以确定符号的原始类型。 请注意，某些符号可能不具有原始类型的修改类型。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)