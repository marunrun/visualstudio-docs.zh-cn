---
title: 'Idiasymbol:: Get_virtualbaseoffset |Microsoft Docs'
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
ms.openlocfilehash: f1cb4a34f9947d2f5ee50488876d44042b4cb228
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64830832"
---
# <a name="idiasymbolgetvirtualbaseoffset"></a>IDiaSymbol::get_virtualBaseOffset
检索虚拟函数的虚函数表中的偏移量。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualBaseOffset ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]虚函数的虚函数表中返回的偏移量。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)