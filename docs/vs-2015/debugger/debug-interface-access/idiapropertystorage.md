---
title: IDiaPropertyStorage | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage interface
ms.assetid: d3197a38-5973-4e56-873e-4f1b84c3f674
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 29832934b848729879ee1ba802c70f85117efd2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62537623"
---
# <a name="idiapropertystorage"></a>IDiaPropertyStorage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

允许你读取 DIA 属性集的持久性属性。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaPropertyStorage : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaPropertyStorage`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaPropertyStorage::Enum](../../debugger/debug-interface-access/idiapropertystorage-enum.md)|获取一个指向枚举数的这组内的属性。|  
|[IDiaPropertyStorage::ReadBOOL](../../debugger/debug-interface-access/idiapropertystorage-readbool.md)|读取`BOOL`属性组中的值。|  
|[IDiaPropertyStorage::ReadBSTR](../../debugger/debug-interface-access/idiapropertystorage-readbstr.md)|读取`BSTR`属性组中的值。|  
|[IDiaPropertyStorage::ReadDWORD](../../debugger/debug-interface-access/idiapropertystorage-readdword.md)|读取`DWORD`属性组中的值。|  
|[IDiaPropertyStorage::ReadLONG](../../debugger/debug-interface-access/idiapropertystorage-readlong.md)|读取`LONG`属性组中的值。|  
|[IDiaPropertyStorage::ReadMultiple](../../debugger/debug-interface-access/idiapropertystorage-readmultiple.md)|读取属性集中的属性值。|  
|[IDiaPropertyStorage::ReadPropertyNames](../../debugger/debug-interface-access/idiapropertystorage-readpropertynames.md)|获取相对应的字符串名称给定属性标识符。|  
|[IDiaPropertyStorage::ReadULONGLONG](../../debugger/debug-interface-access/idiapropertystorage-readulonglong.md)|读取`ULONGLONG`属性组中的值。|  
  
## <a name="remarks"></a>备注  
 属性集内的每个属性由属性标识符 (ID)，4 字节`ULONG`该集的唯一值。 通过公开的属性`IDiaPropertyStorage`接口对应的父接口中的可用属性。 例如的属性[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)可以通过名称访问接口`IDiaPropertyStorage`接口 (但，请注意，即使该属性可能是可访问，它并不意味着该属性是有效的特定`IDiaSymbol`对象)。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 通过调用来获取此接口`QueryInterface`另一个接口上的方法。 以下接口可用于查询`IDiaPropertyStorage`接口：  
  
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)  
  
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)  
  
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)  
  
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)  
  
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)  
  
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)  
  
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)  
  
## <a name="example"></a>示例  
 此示例中演示的功能可显示所有属性公开的`IDiaPropertyStorage`对象。 请参阅[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)接口以举例说明如何`IDiaPropertyStorage`接口的均来自[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)接口。  
  
```cpp#  
void PrintPropertyStorage(IDiaPropertyStorage* pPropertyStorage)  
{  
    IEnumSTATPROPSTG* pEnumProps;  
    STATPROPSTG       prop;  
    DWORD             celt = 1;  
  
    if (pPropertyStorage->Enum(&pEnumProps) == S_OK)  
    {  
        while (pEnumProps->Next(celt, &prop, &celt) == S_OK)  
        {  
            PROPSPEC pspec = { PRSPEC_PROPID, prop.propid };  
            PROPVARIANT vt = { VT_EMPTY };  
  
            if (pPropertyStorage->ReadMultiple( 1, &pspec, &vt) == S_OK)  
            {  
                switch( vt.vt ){  
                    case VT_BOOL:  
                        wprintf( L"%32s:\t %s\n", prop.lpwstrName, vt.bVal ? L"true" : L"false" );  
                        break;  
                    case VT_I2:  
                        wprintf( L"%32s:\t %d\n", prop.lpwstrName, vt.iVal );  
                        break;  
                    case VT_UI2:  
                        wprintf( L"%32s:\t %d\n", prop.lpwstrName, vt.uiVal );  
                        break;  
                    case VT_I4:  
                        wprintf( L"%32s:\t %d\n", prop.lpwstrName, vt.intVal );  
                        break;  
                    case VT_UI4:  
                        wprintf( L"%32s:\t 0x%0x\n", prop.lpwstrName, vt.uintVal );  
                        break;  
                    case VT_UI8:  
                        wprintf( L"%32s:\t 0x%x\n", prop.lpwstrName, vt.uhVal.QuadPart );  
                        break;  
                    case VT_BSTR:  
                        wprintf( L"%32s:\t %s\n", prop.lpwstrName, vt.bstrVal );  
                        break;  
                    case VT_UNKNOWN:  
                        wprintf( L"%32s:\t %p\n", prop.lpwstrName, vt.punkVal );  
                        break;  
                    case VT_SAFEARRAY:  
                        break;  
                    default:  
                       break;  
                }  
                VariantClear((VARIANTARG*) &vt);  
            }  
        }  
        pEnumProps->Release();  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)   
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)   
 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)   
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)   
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)   
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
