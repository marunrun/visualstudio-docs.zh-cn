---
title: IDiaInjectedSource | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource interface
ms.assetid: 75192c5c-812d-4675-9dc5-4c2cff3ba503
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 994f454372883f2516d1eab03bf1152693969b16
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743307"
---
# <a name="idiainjectedsource"></a>IDiaInjectedSource
访问存储在 DIA 数据源中的注入的源代码。

## <a name="syntax"></a>语法

```
IDiaInjectedSource : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示 `IDiaInjectedSource` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaInjectedSource::get_crc](../../debugger/debug-interface-access/idiainjectedsource-get-crc.md)|检索从源代码字节计算得出的循环冗余检查（CRC）。|
|[IDiaInjectedSource::get_length](../../debugger/debug-interface-access/idiainjectedsource-get-length.md)|检索代码的字节数。|
|[IDiaInjectedSource::get_filename](../../debugger/debug-interface-access/idiainjectedsource-get-filename.md)|检索源的文件名。|
|[IDiaInjectedSource::get_objectFilename](../../debugger/debug-interface-access/idiainjectedsource-get-objectfilename.md)|检索源所编译到的对象文件名。|
|[IDiaInjectedSource::get_virtualFilename](../../debugger/debug-interface-access/idiainjectedsource-get-virtualfilename.md)|检索为非文件源代码指定的名称;也就是说，注入的代码。|
|[IDiaInjectedSource::get_sourceCompression](../../debugger/debug-interface-access/idiainjectedsource-get-sourcecompression.md)|检索使用的源压缩的指示器。|
|[IDiaInjectedSource::get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)|检索源代码字节。|

## <a name="remarks"></a>备注
注入的源是编译期间注入的文本。 这并不意味着在中C++使用了预处理器 `#include`。

## <a name="notes-for-callers"></a>调用方说明
通过调用[IDiaEnumInjectedSources：： Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)或[IDiaEnumInjectedSources：： Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)方法获取此接口。 有关获取 `IDiaInjectedSource` 接口的示例，请参阅[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)接口。

## <a name="example"></a>示例
此示例显示 `IDiaInjectedSource` 接口中可用的数据。 有关使用[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)接口的替代方法，请参阅[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)接口中的示例。

```C++
void PrintInjectedSource(IDiaInjectedSource* pSource)
{
    ULONGLONG codeLength      = 0;
    DWORD     crc             = 0;
    DWORD     compressionType = 0;
    BSTR      sourceFilename  = NULL;
    BSTR      objectFilename  = NULL;
    BSTR      virtualFilename = NULL;

    std::cout << "Injected Source:" << std::endl;
    if (pSource != NULL)
    {
        if (pSource->get_crc(&crc) == S_OK &&
            pSource->get_sourceCompression(&compressionType) == S_OK &&
            pSource->get_length(&codeLength) == S_OK)
        {
            wprintf(L"  crc = %lu\n", crc);
            wprintf(L"  code length = %I64u\n",codeLength);
            wprintf(L"  compression type code = %lu\n", compressionType);
        }

        wprintf(L"  source filename: ");
        if (pSource->get_filename(&sourceFilename) == S_OK)
        {
            wprintf(L"%s", sourceFilename);
        }
        else
        {
            wprintf(L"<none>");
        }
        wprintf(L"\n");

        wprintf(L"  object filename: ");
        if (pSource->get_filename(&objectFilename) == S_OK)
        {
            wprintf(L"%s", objectFilename);
        }
        else
        {
            wprintf(L"<none>");
        }
        wprintf(L"\n");

        wprintf(L"  virtual filename: ");
        if (pSource->get_filename(&virtualFilename) == S_OK)
        {
            wprintf(L"%s", virtualFilename);
        }
        else
        {
            wprintf(L"<none>");
        }
        wprintf(L"\n");

        SysFreeString(sourceFilename);
        SysFreeString(objectFilename);
        SysFreeString(virtualFilename);
    }
}
```

## <a name="requirements"></a>要求
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumInjectedSources::Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)
- [IDiaEnumInjectedSources::Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
