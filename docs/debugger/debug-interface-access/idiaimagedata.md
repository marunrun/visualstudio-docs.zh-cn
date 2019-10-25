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
ms.openlocfilehash: 75a81ae23db90b06915e7090a9f2918be3ff18ae
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743396"
---
# <a name="idiaimagedata"></a>IDiaImageData
公开模块或图像的基位置和内存偏移量的详细信息。

## <a name="syntax"></a>语法

```
IDiaImageData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示 `IDiaImageData` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaImageData::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiaimagedata-get-relativevirtualaddress.md)|检索模块相对于应用程序的虚拟内存中的位置。|
|[IDiaImageData::get_virtualAddress](../../debugger/debug-interface-access/idiaimagedata-get-virtualaddress.md)|检索映像的虚拟内存中的位置。|
|[IDiaImageData::get_imageBase](../../debugger/debug-interface-access/idiaimagedata-get-imagebase.md)|检索图像应基于的内存位置。|

## <a name="remarks"></a>备注
某些调试流（XDATA，PDATA）包含也存储在图像中的数据的副本。 可以查询这些流数据对象的 `IDiaImageData` 接口。 有关详细信息，请参阅本主题中的 "调用方的说明" 部分。

## <a name="notes-for-callers"></a>调用方说明
通过对[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)对象调用 `QueryInterface` 获取此接口。 请注意，并非所有调试流都支持 `IDiaImageData` 接口。 例如，当前只有 XDATA 和 PDATA 流支持 `IDiaImageData` 接口。

## <a name="example"></a>示例
此示例将在所有调试流中搜索支持 `IDiaImageData` 接口的任何流。 如果找到这样的流，则会显示有关此流的某些信息。

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
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
