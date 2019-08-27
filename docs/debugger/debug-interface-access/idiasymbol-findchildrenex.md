---
title: IDiaSymbol::findChildrenEx |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenEx
ms.assetid: 6e045045-da8c-4338-9423-81a1ca20c405
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b833353beb009bb4eabbf000d45e0eb44a5794f
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62837870"
---
# <a name="idiasymbolfindchildrenex"></a>IDiaSymbol::findChildrenEx
检索的符号的子级。 返回本地符号包括实时范围信息，如果程序通过优化编译上。

## <a name="syntax"></a>语法

```C++
HRESULT findChildrenEx ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `symtag`

[in]指定要检索的子对象的符号标记中定义[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)。 设置为`SymTagNull`要检索的所有子级。

 `name`

[in]指定要检索的子对象的名称。 设置为`NULL`要检索的所有子级。

 `compareFlags`

[in]指定要应用到匹配的名称的比较选项。 中的值[NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)枚举可以单独或组合使用。

 `ppResult`

[out]返回[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)检索包含子符号的列表的对象。

## <a name="return-value"></a>返回值
 返回`S_OK`如果至少一个子级的符号已找到，或者返回`S_FALSE`是否不发现了任何子级; 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法是扩展的版本[idiasymbol:: Findchildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)。

## <a name="requirements"></a>要求
 标头：dia2.h

 库： diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)