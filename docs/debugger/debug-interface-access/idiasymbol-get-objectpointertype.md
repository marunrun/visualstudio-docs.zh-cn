---
title: IDiaSymbol：： get_objectPointerType |Microsoft Docs
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
ms.openlocfilehash: e4254a121ce29578438f4ee7264345aa30bafd7e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739621"
---
# <a name="idiasymbolget_objectpointertype"></a>IDiaSymbol::get_objectPointerType
检索类方法的对象指针的类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_objectPointerType ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，该对象表示类方法的对象指针。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 此属性仅适用于[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)类型为 `SymTagFunctionType` 的符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)