---
title: IDiaEnumTables::Item | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Item method
ms.assetid: d65ab262-10c6-48ce-95a3-b5e4cb2c85af
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9eec94a5a02eda8fe9b1b3bf8f76f5050ab1e020
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423863"
---
# <a name="idiaenumtablesitem"></a>IDiaEnumTables::Item
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

通过索引或名称检索表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Item (   
   VARIANT     index,  
   IDiaTable** table  
);  
```  
  
#### <a name="parameters"></a>参数  
 `index`  
 中要检索的 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 的索引或名称。 如果使用整数变量，则该值必须介于0到 `count` -1 之间，其中 `count` 是 [IDiaEnumTables：： get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md) 方法返回的。  
  
 `table`  
 弄返回一个 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 对象，该对象表示所需的表。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果指定字符串变量，则该字符串将命名特定表。 该名称应为 [ (调试接口访问 SDK) 的常量 ](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)中定义的表名称之一。  
  
## <a name="example"></a>示例  
  
```cpp#  
VARIANT var;  
var.vt = VT_BSTR;  
var.bstrVal = SysAllocString(DiaTable_Symbols );  
IDiaTable* pTable;  
pEnumTables->Item( var, &pTable );  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)   
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)   
 [IDiaEnumTables：： get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)   
 [常量（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)
