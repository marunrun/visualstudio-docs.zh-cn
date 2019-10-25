---
title: IDiaSymbol：： get_unalignedType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_unalignedType method
ms.assetid: fdcb38fb-490e-4d15-b4e5-3770043a366c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 92d849860d4c91557f01a26f107782772c508caa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739022"
---
# <a name="idiasymbolget_unalignedtype"></a>IDiaSymbol::get_unalignedType
检索一个标志，该标志指定用户定义的数据类型是否是不对齐的。

## <a name="syntax"></a>语法

```C++
HRESULT get_unalignedType ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果用户定义数据类型是未对齐的，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)