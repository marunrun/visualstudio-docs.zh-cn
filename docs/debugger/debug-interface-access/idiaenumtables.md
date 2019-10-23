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
ms.openlocfilehash: d505219468f802a3eff9df0ad766fd1a353d5166
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743702"
---
# <a name="idiaenumtables"></a>IDiaEnumTables
枚举数据源中包含的各个表。

## <a name="syntax"></a>语法

```
IDiaEnumTables : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示 `IDiaEnumTables` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaEnumTables::get__NewEnum](../../debugger/debug-interface-access/idiaenumtables-get-newenum.md)|检索此枚举器的[IEnumVARIANT 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant)版本。|
|[IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)|检索表的数目。|
|[IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)|通过索引或名称检索表。|
|[IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)|检索枚举序列中指定数量的表。|
|[IDiaEnumTables::Skip](../../debugger/debug-interface-access/idiaenumtables-skip.md)|跳过枚举序列中指定数量的表。|
|[IDiaEnumTables::Reset](../../debugger/debug-interface-access/idiaenumtables-reset.md)|将枚举序列重置到开始处。|
|[IDiaEnumTables::Clone](../../debugger/debug-interface-access/idiaenumtables-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方说明
通过调用[IDiaSession：： getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)方法获取此接口。

## <a name="example"></a>示例
此示例演示如何从会话获取 `IDiaEnumTables` 接口。 有关使用表的更完整示例，请参阅[IDiaTable](../../debugger/debug-interface-access/idiatable.md)接口。

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
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
