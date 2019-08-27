---
title: IDiaSymbol::get_udtKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_udtKind method
ms.assetid: 4002f887-aea6-4475-b302-67c57079fe0a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34faf217f77bd30ba707f5ae17886b05dac8ab4f
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64796637"
---
# <a name="idiasymbolgetudtkind"></a>IDiaSymbol::get_udtKind
检索用户定义类型 (UDT) 的多样性。

## <a name="syntax"></a>语法

```C++
HRESULT get_udtKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个值从[UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)指定 UDT 类型的枚举： 结构、 类或联合。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)