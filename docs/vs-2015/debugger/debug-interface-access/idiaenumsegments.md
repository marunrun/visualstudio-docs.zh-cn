---
title: IDiaEnumSegments | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments interface
ms.assetid: 0c9edd5e-b9ce-43e1-a791-cd4c5d16d923
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bfd82fa284e76ecbbc7553f83d98303dd1ff78ff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684427"
---
# <a name="idiaenumsegments"></a>IDiaEnumSegments
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举数据源中包含的各个段。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaEnumSegments : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDiaEnumSegments` 。  
  
|方法|说明|  
|------------|-----------------|  
|[IDiaEnumSegments::get__NewEnum](../../debugger/debug-interface-access/idiaenumsegments-get-newenum.md)|检索此枚举器的 [IEnumVARIANT 接口](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e) 版本。|  
|[IDiaEnumSegments::get_Count](../../debugger/debug-interface-access/idiaenumsegments-get-count.md)|检索段数。|  
|[IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)|通过索引检索段。|  
|[IDiaEnumSegments::Next](../../debugger/debug-interface-access/idiaenumsegments-next.md)|检索枚举序列中指定数量的段。|  
|[IDiaEnumSegments::Skip](../../debugger/debug-interface-access/idiaenumsegments-skip.md)|跳过枚举序列中指定数量的段。|  
|[IDiaEnumSegments::Reset](../../debugger/debug-interface-access/idiaenumsegments-reset.md)|将枚举序列重置到开始处。|  
|[IDiaEnumSegments::Clone](../../debugger/debug-interface-access/idiaenumsegments-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方说明  
 通过 `QueryInterface` 对 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 对象调用方法获取此接口。 参阅示例了解详细信息。  
  
## <a name="example"></a>示例  
 此示例演示如何 `IDiaEnumSections` 从表中获取接口。 有关使用段的更完整示例，请参阅 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) 接口。  
  
```cpp#  
void ShowSegments(IDiaTable *pTable, IDiaSession *pSession)  
{  
    CComPtr<IDiaEnumSegments> pSegments;  
    if ( SUCCEEDED( pTable->QueryInterface(  
                                __uuidof( IDiaEnumSegments ),  
                                (void**)&pSegments )  
                  )  
       )  
    {  
        // Do something with this enumeration  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： Dia2  
  
 库： diaguids  
  
 DLL： msdia80.dll  
  
## <a name="see-also"></a>另请参阅  
 [接口 (调试接口访问 SDK) ](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)   
 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
