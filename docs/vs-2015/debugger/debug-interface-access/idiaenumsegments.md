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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65684427"
---
# <a name="idiaenumsegments"></a>IDiaEnumSegments
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举数据源中包含的各个部分。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaEnumSegments : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaEnumSegments`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaEnumSegments::get__NewEnum](../../debugger/debug-interface-access/idiaenumsegments-get-newenum.md)|检索[IEnumVARIANT 接口](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e)此枚举器的版本。|  
|[IDiaEnumSegments::get_Count](../../debugger/debug-interface-access/idiaenumsegments-get-count.md)|检索的段数。|  
|[IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)|通过索引中检索一个段。|  
|[IDiaEnumSegments::Next](../../debugger/debug-interface-access/idiaenumsegments-next.md)|检索指定的数目的枚举序列中的段。|  
|[IDiaEnumSegments::Skip](../../debugger/debug-interface-access/idiaenumsegments-skip.md)|将跳过枚举序列中的指定的段数。|  
|[IDiaEnumSegments::Reset](../../debugger/debug-interface-access/idiaenumsegments-reset.md)|将枚举序列重置到开头。|  
|[IDiaEnumSegments::Clone](../../debugger/debug-interface-access/idiaenumsegments-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方的说明  
 通过调用来获取此接口`QueryInterface`方法[IDiaTable](../../debugger/debug-interface-access/idiatable.md)对象。 请参阅详细信息的示例。  
  
## <a name="example"></a>示例  
 此示例演示如何获取`IDiaEnumSections`表中的接口。 使用段的更完整示例，请参阅[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)接口。  
  
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
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)   
 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
