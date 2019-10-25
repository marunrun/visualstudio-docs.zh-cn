---
title: IDiaSymbol：： get_types |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_types method
ms.assetid: 5f056e0c-e15b-4e00-8f78-aadc8574f7ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d23ea3c4d885b3f7575c998999814d0808d03bc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739057"
---
# <a name="idiasymbolget_types"></a>IDiaSymbol::get_types
检索此符号的编译器特定类型的数组。

## <a name="syntax"></a>语法

```C++
HRESULT get_types ( 
   DWORD       cTypes,
   DWORD*      pcTypes,
   IDiaSymbol* types[]
);
```

#### <a name="parameters"></a>参数
 `cTypes`

中用于保存数据的缓冲区大小。

 `pcTypes`

弄返回已写入的类型的数目，或者，如果 `types` 参数 `NULL`，则返回可用的类型总数。

 `types[]`

弄要使用表示此符号的所有类型的[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象填充的数组。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)