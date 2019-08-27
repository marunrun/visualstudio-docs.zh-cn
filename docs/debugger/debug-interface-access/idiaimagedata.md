---
title: IDiaImageData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData interface
ms.assetid: b696f350-fc08-4352-9287-a15e87512c1e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1e3dd8c395c59bc3255c1c9ee55837466c1cef7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828511"
---
# <a name="idiaimagedata"></a>IDiaImageData
公开的模块或映像的基的位置和内存偏移量的详细信息。

## <a name="syntax"></a>语法

```
IDiaImageData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaImageData`。

|方法|描述|
|------------|-----------------|
|[IDiaImageData::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiaimagedata-get-relativevirtualaddress.md)|检索虚拟内存中的位置相对于应用程序的模块。|
|[IDiaImageData::get_virtualAddress](../../debugger/debug-interface-access/idiaimagedata-get-virtualaddress.md)|检索虚拟内存中的映像的位置。|
|[IDiaImageData::get_imageBase](../../debugger/debug-interface-access/idiaimagedata-get-imagebase.md)|检索其中应基于映像的内存位置。|

## <a name="remarks"></a>备注
某些调试流 （XDATA、 PDATA） 包含也存储在映像中的数据的副本。 这些流式传输的数据可以用于查询对象`IDiaImageData`接口。 请参阅本主题的详细信息"的调用方备注"部分。

## <a name="notes-for-callers"></a>调用方的说明
通过调用来获取此接口`QueryInterface`上[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)对象。 请注意，并非所有调试流支持`IDiaImageData`接口。 例如，当前仅 XDATA 和 PDATA 流支持`IDiaImageData`接口。

## <a name="example"></a>示例
此示例将搜索所有支持的任何流的调试流`IDiaImageData`接口。 如果找到此类流，则显示该流的一些信息。

```C++
void ShowImageData(IDiaSession *pSession)
{
    if (pSession != NULL)
    {
        CComPtr<IDiaEnumDebugStreams> pStreamsList;
        HRESULT hr;

        hr = pSession->getEnumDebugStreams(&pStreamsList);
        if (SUCCEEDED(hr))
        {
            LONG numStreams = 0;
            hr = pStreamsList->get_Count(&numStreams);
            if (SUCCEEDED(hr))
            {
                ULONG fetched = 0;
                for (LONG i = 0; i < numStreams; i++)
                {
                    CComPtr<IDiaEnumDebugStreamData> pStream;
                    hr = pStreamsList->Next(1,&pStream,&fetched);
                    if (fetched == 1)
                    {
                        CComPtr<IDiaImageData> pImageData;
                        hr = pStream->QueryInterface(__uuidof(IDiaImageData),
                                                     (void **)&pImageData);
                        if (SUCCEEDED(hr))
                        {
                            CComBSTR name;
                            hr = pStream->get_name(&name);
                            if (SUCCEEDED(hr))
                            {
                                wprintf(L"Stream %s:\n",(BSTR)name);
                            }
                            else
                            {
                                wprintf(L"Failed to get name of stream\n");
                            }

                            ULONGLONG imageBase = 0;
                            if (pImageData->get_imageBase(&imageBase) == S_OK)
                            {
                                wprintf(L"  image base = 0x%0I64x\n",imageBase);
                            }

                            DWORD relVA = 0;
                            if (pImageData->get_relativeVirtualAddress(&relVA) == S_OK)
                            {
                                wprintf(L"  relative virtual address = 0x%08lx\n",relVA);
                            }

                            ULONGLONG va = 0;
                            if (pImageData->get_virtualAddress(&va) == S_OK)
                            {
                                wprintf(L"  virtual address = 0x%0I64x\n", va);
                            }
                        }
                    }
                }
            }
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
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
