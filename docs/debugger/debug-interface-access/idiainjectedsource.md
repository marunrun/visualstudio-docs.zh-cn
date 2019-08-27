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
ms.openlocfilehash: 2e8956fb7da61519ed9d0939da087ce8a4181ac1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839870"
---
# <a name="idiainjectedsource"></a>IDiaInjectedSource
访问注入 DIA 数据源中存储的源代码。

## <a name="syntax"></a>语法

```
IDiaInjectedSource : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaInjectedSource`。

|方法|描述|
|------------|-----------------|
|[IDiaInjectedSource::get_crc](../../debugger/debug-interface-access/idiainjectedsource-get-crc.md)|检索从源代码的字节计算的循环冗余检查 (CRC)。|
|[IDiaInjectedSource::get_length](../../debugger/debug-interface-access/idiainjectedsource-get-length.md)|检索的代码的字节数。|
|[IDiaInjectedSource::get_filename](../../debugger/debug-interface-access/idiainjectedsource-get-filename.md)|检索源的文件名称。|
|[IDiaInjectedSource::get_objectFilename](../../debugger/debug-interface-access/idiainjectedsource-get-objectfilename.md)|检索到的源已编译的对象文件名称。|
|[IDiaInjectedSource::get_virtualFilename](../../debugger/debug-interface-access/idiainjectedsource-get-virtualfilename.md)|检索为非文件源的代码; 指定的名称也就是说，注入的代码。|
|[IDiaInjectedSource::get_sourceCompression](../../debugger/debug-interface-access/idiainjectedsource-get-sourcecompression.md)|检索源所使用的压缩的指示器。|
|[IDiaInjectedSource::get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)|检索源代码字节。|

## <a name="remarks"></a>备注
插入的源是在编译过程中注入的文本。 这并不意味着预处理器`#include`中使用C++。

## <a name="notes-for-callers"></a>调用方的说明
通过调用来获取此接口[idiaenuminjectedsources:: Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)或[idiaenuminjectedsources:: Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)方法。 请参阅[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)接口以举例说明获取`IDiaInjectedSource`接口。

## <a name="example"></a>示例
此示例中显示的数据可从`IDiaInjectedSource`接口。 另一种方法使用[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)接口，请参阅中的示例[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)接口。

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
标头：dia2.h

库： diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumInjectedSources::Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)
- [IDiaEnumInjectedSources::Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
