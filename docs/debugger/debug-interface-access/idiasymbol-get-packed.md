---
title: 'Idiasymbol:: Get_packed |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_packed method
ms.assetid: e42ff368-56c4-49a2-8676-f80e349efa21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 91e99da7832bb2a0e067de6eb3c09f90255eaf32
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64785842"
---
# <a name="idiasymbolgetpacked"></a>IDiaSymbol::get_packed
检索指定用户定义数据类型 (UDT) 是否打包的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_packed ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`打包用户定义的类型; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 打包的 UDT 的所有成员都位于尽可能靠近且没有干扰填充到内存边界对齐方式。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)