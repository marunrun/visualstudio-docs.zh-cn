---
title: IDiaEnumSymbols |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols interface
ms.assetid: 649f7bfd-86ac-49a5-8533-aff77e1bc62e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 44be5f88542d867d8baf25fbc3cdd3c060231d7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833397"
---
# <a name="idiaenumsymbols"></a>IDiaEnumSymbols
枚举数据源中包含的各种符号。

## <a name="syntax"></a>语法

```
IDiaEnumSymbols : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaEnumSymbols`。

|方法|描述|
|------------|-----------------|
|[IDiaEnumSymbols::get__NewEnum](../../debugger/debug-interface-access/idiaenumsymbols-get-newenum.md)|检索`IEnumVARIANT Interface`此枚举器的版本。|
|[IDiaEnumSymbols::get_Count](../../debugger/debug-interface-access/idiaenumsymbols-get-count.md)|检索的符号的数量。|
|[IDiaEnumSymbols::Item](../../debugger/debug-interface-access/idiaenumsymbols-item.md)|通过索引中检索一个符号。|
|[IDiaEnumSymbols::Next](../../debugger/debug-interface-access/idiaenumsymbols-next.md)|检索指定的数目的枚举序列中的符号。|
|[IDiaEnumSymbols::Skip](../../debugger/debug-interface-access/idiaenumsymbols-skip.md)|将跳过指定的数目的枚举序列中的符号。|
|[IDiaEnumSymbols::Reset](../../debugger/debug-interface-access/idiaenumsymbols-reset.md)|将枚举序列重置到开头。|
|[IDiaEnumSymbols::Clone](../../debugger/debug-interface-access/idiaenumsymbols-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|

## <a name="remarks"></a>备注
此接口提供特定类型的符号，例如，按分组的符号`SymTagUDT`（用户定义类型） 或`SymTagBaseClass`。 要与符号按地址分组，请使用[IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)接口。

## <a name="notes-for-callers"></a>调用方的说明
通过调用以下方法来获取此接口：

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

- [IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)

## <a name="example"></a>示例
此示例演示如何获取`IDiaEnumSymbols`接口，然后使用该枚举到列表的用户定义类型 (Udt)。

> [!NOTE]
> `CDiaBSTR` 是一个类，包装`BSTR`和实例化超出范围时释放该字符串将自动处理。

```C++
void ShowUDTs(IDiaSymbol *pGlobals)
{
    CComPtr<IDiaEnumSymbols> pEnum;
    CComPtr<IDiaSymbol> pSymbol;
    HRESULT hr;

    hr = pGlobals->findChildren(SymTagUDT,
                                NULL,
                                nsfCaseInsensitive | nsfUndecoratedName,
                                &pEnum);
    if (hr == S_OK)
    {
        while ( SUCCEEDED( hr = pEnum->Next( 1, &pSymbol, &celt ) ) &&
                celt == 1 )
        {
            CDiaBSTR name;
            if ( pSymbol->get_name( &name ) != S_OK )
                Fatal( "get_name" );
            printf( "Found UDT: %ws\n", name );
            pSymbol = 0;
        }
    }
}
```

## <a name="requirements"></a>要求
标头：dia2.h

库： diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
