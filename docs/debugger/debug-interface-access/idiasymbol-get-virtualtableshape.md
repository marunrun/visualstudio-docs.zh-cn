---
title: IDiaSymbol::get_virtualTableShape | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualTableShape method
ms.assetid: 92360cbd-0761-446e-93f9-04dc8f4b66c6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bcbbf5463486c0c4bb2417793d3f37bee2d121c2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738823"
---
# <a name="idiasymbolget_virtualtableshape"></a>IDiaSymbol::get_virtualTableShape
检索用户定义类型的虚拟表的类型的符号接口。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualTableShape ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，该对象表示用户定义类型的虚拟表。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)