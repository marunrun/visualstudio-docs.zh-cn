---
title: IDiaEnumTables | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables interface
ms.assetid: 016190c5-09e4-48f2-bf60-9b02603a03e0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 20bd652437f0c1765686afc1d93a81bc9110236d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829129"
---
# <a name="idiaenumtables"></a>IDiaEnumTables
枚举数据源中包含的各个表。

## <a name="syntax"></a>语法

```
IDiaEnumTables : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDiaEnumTables`。

|方法|描述|
|------------|-----------------|
|[IDiaEnumTables::get__NewEnum](../../debugger/debug-interface-access/idiaenumtables-get-newenum.md)|检索[IEnumVARIANT 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant)此枚举器的版本。|
|[IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)|检索表的数目。|
|[IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)|检索通过名称或索引的表。|
|[IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)|检索指定的数目的枚举序列中的表。|
|[IDiaEnumTables::Skip](../../debugger/debug-interface-access/idiaenumtables-skip.md)|跳过枚举序列中的表的指定的数目。|
|[IDiaEnumTables::Reset](../../debugger/debug-interface-access/idiaenumtables-reset.md)|将枚举序列重置到开头。|
|[IDiaEnumTables::Clone](../../debugger/debug-interface-access/idiaenumtables-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方的说明
通过调用来获取此接口[idiasession:: Getenumtables](../../debugger/debug-interface-access/idiasession-getenumtables.md)方法。

## <a name="example"></a>示例
此示例演示如何获取`IDiaEnumTables`从会话的接口。 使用表的更完整示例，请参阅[IDiaTable](../../debugger/debug-interface-access/idiatable.md)接口。

```C++
void ShowTableNames(IDiaSession *pSession)
{
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    // Do something with table
}
```

## <a name="requirements"></a>要求
标头：dia2.h

库： diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
