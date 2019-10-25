---
title: IDiaSymbol::findChildrenExByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenExByVA
ms.assetid: 29080009-36e4-4697-acd7-50f2e3e1bf1b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d9cc9f540b200ff6fdf4736b6a0bf64175a5ee3e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741247"
---
# <a name="idiasymbolfindchildrenexbyva"></a>IDiaSymbol::findChildrenExByVA
检索在指定的虚拟地址中有效的符号子级。

## <a name="syntax"></a>语法

```C++
HRESULT findChildrenExByVA ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   DWORD             address,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `symtag`

中指定要检索的子级的符号标记，如[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)中所定义。 设置为要检索的所有子级 `SymTagNull`。

 `name`

中指定要检索的子项的名称。 设置为要检索的所有子级 `NULL`。

 `compareFlags`

中指定要应用于名称匹配的比较选项。 [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)枚举中的值可以单独使用，也可以组合使用。

 `address`

中指定虚拟地址。

 `ppResult`

弄返回一个[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)对象，该对象包含所检索到的子符号的列表。

## <a name="return-value"></a>返回值
 如果找到至少一个符号子级，则返回 `S_OK`; 如果未找到任何子级，则返回 `S_FALSE`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 返回的本地符号包含实时范围信息。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)