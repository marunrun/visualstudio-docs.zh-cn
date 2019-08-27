---
title: 'Idiasymbol:: Get_objectpointertype |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_objectPointerType method
ms.assetid: bce193b9-67b0-4c35-96e5-6a664937322e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 69dac79a040a8eff68c36c82b9a85935d969b5ec
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64808902"
---
# <a name="idiasymbolgetobjectpointertype"></a>IDiaSymbol::get_objectPointerType
检索类方法的对象指针的类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_objectPointerType ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示类方法的对象指针。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 此属性仅适用于包含符号[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)类型的`SymTagFunctionType`。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)