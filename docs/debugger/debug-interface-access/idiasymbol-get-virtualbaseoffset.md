---
title: IDiaSymbol：： get_virtualBaseOffset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualBaseOffset method
ms.assetid: 103b034f-36c4-42d5-aa34-1449a1e66d03
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c72c605b47a5f34542b46cae9943b03c7072b1f5
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738870"
---
# <a name="idiasymbolget_virtualbaseoffset"></a>IDiaSymbol::get_virtualBaseOffset
检索虚拟函数的虚拟函数表中的偏移量。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualBaseOffset ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回虚拟函数的虚拟函数表中的偏移量。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)