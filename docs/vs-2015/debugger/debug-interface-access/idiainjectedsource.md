---
title: IDiaInjectedSource | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource interface
ms.assetid: 75192c5c-812d-4675-9dc5-4c2cff3ba503
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 59bd1cd56ee36c5e4164549df987f789aafe32e1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203610"
---
# <a name="idiainjectedsource"></a>IDiaInjectedSource
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

访问存储在 DIA 数据源中的注入的源代码。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaInjectedSource : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDiaInjectedSource` 。  
  
|方法|说明|  
|------------|-----------------|  
|[IDiaInjectedSource::get_crc](../../debugger/debug-interface-access/idiainjectedsource-get-crc.md)|检索循环冗余检查 (CRC) 从源代码字节计算得出的。|  
|[IDiaInjectedSource::get_length](../../debugger/debug-interface-access/idiainjectedsource-get-length.md)|检索代码的字节数。|  
|[IDiaInjectedSource::get_filename](../../debugger/debug-interface-access/idiainjectedsource-get-filename.md)|检索源的文件名。|  
|[IDiaInjectedSource::get_objectFilename](../../debugger/debug-interface-access/idiainjectedsource-get-objectfilename.md)|检索源所编译到的对象文件名。|  
|[IDiaInjectedSource::get_virtualFilename](../../debugger/debug-interface-access/idiainjectedsource-get-virtualfilename.md)|检索为非文件源代码指定的名称;也就是说，注入的代码。|  
|[IDiaInjectedSource::get_sourceCompression](../../debugger/debug-interface-access/idiainjectedsource-get-sourcecompression.md)|检索使用的源压缩的指示器。|  
|[IDiaInjectedSource::get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)|检索源代码字节。|  
  
## <a name="remarks"></a>备注  
 注入的源是编译期间注入的文本。 这并不意味着 `#include` c + + 中使用的预处理器。  
  
## <a name="notes-for-callers"></a>调用方说明  
 通过调用 [IDiaEnumInjectedSources：： Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md) 或 [IDiaEnumInjectedSources：： Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md) 方法获取此接口。 有关获取接口的示例，请参阅 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) 接口 `IDiaInjectedSource` 。  
  
## <a name="example"></a>示例  
 此示例显示了接口中可用的数据 `IDiaInjectedSource` 。 有关使用 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md) 接口的替代方法，请参阅 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) 接口中的示例。  
  
```cpp#  
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
  
 DLL： msdia80.dll  
  
## <a name="see-also"></a>另请参阅  
 [接口 (调试接口访问 SDK) ](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaEnumInjectedSources：： Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)   
 [IDiaEnumInjectedSources：： Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)   
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
