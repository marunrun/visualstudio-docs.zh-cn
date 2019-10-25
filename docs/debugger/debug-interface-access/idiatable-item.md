---
title: IDiaTable：： Item |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::Item method
ms.assetid: eae11b26-4807-400c-be25-e85bbc0c6b20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d402f5ad54d5c0f487cebb3a8c53f68d17828ed4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738718"
---
# <a name="idiatableitem"></a>IDiaTable::Item
检索对表中指定项的引用。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD      index,
   IUnknown** element
);
```

#### <a name="parameters"></a>参数
 `index`

中范围0到 `count`-1 的表项的索引，其中 `count` 由[IDiaTable：： get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)方法返回。

 `element`

弄返回一个 `IUnknown` 对象，该对象表示指定的表项。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 表表示对象的集合。 元素参数可以强制转换为相应的接口，具体取决于这些对象。 例如，如果表包含[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)对象，则可以将元素参数强制转换为 `IDiaSegment` 接口。

 在[IDiaTable](../../debugger/debug-interface-access/idiatable.md)接口中调用相应枚举器接口的 `QueryInterface` 方法，并使用枚举器的特定方法访问表内容，这种方法更常见。 有关示例，请参阅[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)接口。

## <a name="see-also"></a>请参阅
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)