---
title: IDiaEnumInjectedSources | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources interface
ms.assetid: f97e2392-22e1-48da-b7ce-ad94c8b684b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: feaf5d372279c6ab24053058a14aba4b3a71fd78
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744463"
---
# <a name="idiaenuminjectedsources"></a>IDiaEnumInjectedSources
枚举数据源中包含的各种注入的源。

## <a name="syntax"></a>语法

```
IDiaEnumInjectedSources : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示 `IDiaEnumInjectedSources` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaEnumInjectedSources::get__NewEnum](../../debugger/debug-interface-access/idiaenuminjectedsources-get-newenum.md)|检索此枚举器的[IEnumVARIANT 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant)版本。|
|[IDiaEnumInjectedSources::get_Count](../../debugger/debug-interface-access/idiaenuminjectedsources-get-count.md)|检索注入的源的数目。|
|[IDiaEnumInjectedSources::Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)|通过索引检索注入的源。|
|[IDiaEnumInjectedSources::Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)|检索枚举序列中指定数量的插入源。|
|[IDiaEnumInjectedSources::Skip](../../debugger/debug-interface-access/idiaenuminjectedsources-skip.md)|跳过枚举序列中指定数量的插入源。|
|[IDiaEnumInjectedSources::Reset](../../debugger/debug-interface-access/idiaenuminjectedsources-reset.md)|将枚举序列重置到开始处。|
|[IDiaEnumInjectedSources::Clone](../../debugger/debug-interface-access/idiaenuminjectedsources-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方说明
通过将[IDiaSession：： findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)方法与特定源文件的名称一起调用，或通过使用 `IDiaEnumInjectedSources` 接口的 GUID 调用[IDiaSession：： getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)方法获取此接口。

## <a name="example"></a>示例
此示例演示如何获取（`GetEnumInjectedSources` 函数）并使用（`DumpAllInjectedSources` 函数） `IDiaEnumInjectedSources` 接口。 有关 `PrintPropertyStorage` 函数的实现，请参阅[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)接口。 有关备用输出，请参阅[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)接口。

```C++

IDiaEnumInjectedSources* GetEnumInjectedSources(IDiaSession *pSession)
{
    IDiaEnumInjectedSources* pUnknown    = NULL;
    REFIID                   iid         = __uuidof(IDiaEnumInjectedSources);
    IDiaEnumTables*          pEnumTables = NULL;
    IDiaTable*               pTable      = NULL;
    ULONG                    celt        = 0;

    if (pSession->getEnumTables(&pEnumTables) != S_OK)
    {
        wprintf(L"ERROR - GetTable() getEnumTables\n");
        return NULL;
    }
    while (pEnumTables->Next(1, &pTable, &celt) == S_OK && celt == 1)
    {
        // There is only one table that matches the given iid
        HRESULT hr = pTable->QueryInterface(iid, (void**)&pUnknown);
        pTable->Release();
        if (hr == S_OK)
        {
            break;
        }
    }
    pEnumTables->Release();
    return pUnknown;
}

void DumpAllInjectedSources( IDiaSession* pSession)
{
    IDiaEnumInjectedSources* pEnumInjSources;

    pEnumInjSources = GetEnumInjectedSources(pSession);
    if (pEnumInjSources != NULL)
    {
        IDiaInjectedSource* pInjSource;
        ULONG celt = 0;

        while(pEnumInjSources->Next(1, &pInjSource, &celt) == S_OK &&
              celt == 1)
        {
            IDiaPropertyStorage *pPropertyStorage;
            if (pInjSource->QueryInterface(__uuidof(IDiaPropertyStorage),
                                          (void **)&pPropertyStorage) == S_OK)
            {
                PrintPropertyStorage(pPropertyStorage);
                pPropertyStorage->Release();
            }
            pInjSource->Release();
        }
        pEnumInjSources->Release();
    }
}
```

## <a name="requirements"></a>要求
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
