---
title: IDiaEnumTables | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables interface
ms.assetid: 016190c5-09e4-48f2-bf60-9b02603a03e0
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 184dadaeecad85f93afc92795e081e9bd9fb06e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696975"
---
# <a name="idiaenumtables"></a>IDiaEnumTables
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举数据源中包含的各个表。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaEnumTables : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDiaEnumTables` 。  
  
|方法|说明|  
|------------|-----------------|  
|[IDiaEnumTables::get__NewEnum](../../debugger/debug-interface-access/idiaenumtables-get-newenum.md)|检索此枚举器的 [IEnumVARIANT 接口](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e) 版本。|  
|[IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)|检索表的数目。|  
|[IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)|通过索引或名称检索表。|  
|[IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)|检索枚举序列中指定数量的表。|  
|[IDiaEnumTables::Skip](../../debugger/debug-interface-access/idiaenumtables-skip.md)|跳过枚举序列中指定数量的表。|  
|[IDiaEnumTables::Reset](../../debugger/debug-interface-access/idiaenumtables-reset.md)|将枚举序列重置到开始处。|  
|[IDiaEnumTables::Clone](../../debugger/debug-interface-access/idiaenumtables-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方说明  
 通过调用 [IDiaSession：： getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md) 方法获取此接口。  
  
## <a name="example"></a>示例  
 此示例演示如何 `IDiaEnumTables` 从会话获取接口。 有关使用表的更完整示例，请参阅 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 接口。  
  
```cpp#  
void ShowTableNames(IDiaSession *pSession)  
{  
    CComPtr<IDiaEnumTables> pTables;  
    if ( FAILED( psession->getEnumTables( &pTables ) ) )  
    {  
        Fatal( "getEnumTables" );  
    }  
    // Do something with table  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： Dia2  
  
 库： diaguids  
  
 DLL： msdia80.dll  
  
## <a name="see-also"></a>另请参阅  
 [接口 (调试接口访问 SDK) ](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
