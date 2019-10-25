---
title: IDiaEnumTables::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Item method
ms.assetid: d65ab262-10c6-48ce-95a3-b5e4cb2c85af
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf2d6b14f17d42a128e59446e27bfc251de40d17
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743752"
---
# <a name="idiaenumtablesitem"></a>IDiaEnumTables::Item
通过索引或名称检索表。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   VARIANT     index,
   IDiaTable** table
);
```

#### <a name="parameters"></a>参数
 `index`

中要检索的[IDiaTable](../../debugger/debug-interface-access/idiatable.md)的索引或名称。 如果使用整数变量，则该变量的范围必须介于0到 `count`-1 之间，其中 `count` 为[IDiaEnumTables：： get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)方法返回的。

 `table`

弄返回一个[IDiaTable](../../debugger/debug-interface-access/idiatable.md)对象，该对象表示所需的表。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 如果指定字符串变量，则该字符串将命名特定表。 名称应为常量中定义的表名称之一[（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)。

## <a name="example"></a>示例

```C++
VARIANT var;
var.vt = VT_BSTR;
var.bstrVal = SysAllocString(DiaTable_Symbols );
IDiaTable* pTable;
pEnumTables->Item( var, &pTable );
```

## <a name="see-also"></a>请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)
- [常量（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)