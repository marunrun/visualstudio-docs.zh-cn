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
ms.openlocfilehash: 03931580f774c29a67771d2251b51825242535c9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829380"
---
# <a name="idiaenumtablesitem"></a>IDiaEnumTables::Item
检索通过索引或名称的表。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   VARIANT     index,
   IDiaTable** table
);
```

#### <a name="parameters"></a>参数
 `index`

[in]索引或名称[IDiaTable](../../debugger/debug-interface-access/idiatable.md)要检索。 如果使用整数变量，则它必须是介于 0 到`count`-1，其中`count`与返回的[idiaenumtables:: Get_count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)方法。

 `table`

[out]返回[IDiaTable](../../debugger/debug-interface-access/idiatable.md)对象，表示所需的表。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 如果指定的字符串变体，则该字符串命名为特定表。 该名称应是表名称之一中定义[常量 (调试接口访问 SDK)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)。

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