---
title: IDiaEnumSectionContribs | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs interface
ms.assetid: 0d6c0632-310f-4a99-8921-58149a1817e3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ede7789fcdba63595cecd6426c8f3ca1a4048e07
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833254"
---
# <a name="idiaenumsectioncontribs"></a>IDiaEnumSectionContribs
枚举数据源中包含的各个部分贡献。

## <a name="syntax"></a>语法

```
IDiaEnumSectionContribs : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaEnumSectionContribs`。

|方法|描述|
|------------|-----------------|
|[IDiaEnumSectionContribs::get__NewEnum](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-newenum.md)|检索[IEnumVARIANT 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant)此枚举器的版本。|
|[IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)|检索部分发布内容的数量。|
|[IDiaEnumSectionContribs::Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md)|通过索引来检索部分发布内容。|
|[IDiaEnumSectionContribs::Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md)|检索指定的数目的枚举序列中的部分发布内容。|
|[IDiaEnumSectionContribs::Skip](../../debugger/debug-interface-access/idiaenumsectioncontribs-skip.md)|跳过枚举序列中的部分发布内容的指定的数目。|
|[IDiaEnumSectionContribs::Reset](../../debugger/debug-interface-access/idiaenumsectioncontribs-reset.md)|将枚举序列重置到开头。|
|[IDiaEnumSectionContribs::Clone](../../debugger/debug-interface-access/idiaenumsectioncontribs-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|

## <a name="remarks"></a>备注

## <a name="note-for-callers"></a>请注意，调用方
获取此接口从[idiasession:: Getenumtables](../../debugger/debug-interface-access/idiasession-getenumtables.md)方法。 请参阅详细信息的示例。

## <a name="example"></a>示例
此示例演示如何获取 (`GetEnumSectionContribs`函数)，并使用 (`ShowSectionContribs`函数)`IDiaEnumSectionContribs`接口。 使用部分发布内容的更完整示例，请参阅[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)接口。

```C++

IDiaEnumSectionContribs* GetEnumSectionContribs(IDiaSession *pSession)
{
    IDiaEnumSectionContribs* pUnknown    = NULL;
    REFIID                   iid         = __uuidof(IDiaEnumSectionContribs);
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

void ShowSectionContribs(IDiaSession *pSession)
{
    IDiaEnumSectionContribs* pEnumSectionContribs;

    pEnumSectionContribs = GetEnumSectionContribs(pSession);
    if (pSectionContrib != NULL)
    {
        IDiaSectionContrib* pSectionContrib;
        ULONG celt = 0;

        while(pEnumSectionContribs->Next(1, &pSectionContrib, &celt) == S_OK &&
              celt == 1)
        {
            PrintSectionContrib(pSectionContrib, pSession);
            pSectionContrib->Release();
        }
        pSectionContrib->Release();
    }
}
```

## <a name="requirements"></a>要求
标头：dia2.h

库： diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
