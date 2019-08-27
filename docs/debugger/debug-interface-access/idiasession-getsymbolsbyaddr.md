---
title: IDiaSession::getSymbolsByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::getSymbolsByAddr method
ms.assetid: eafcc757-b488-487d-a063-ad3703ff42e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f114d14da44d782dbda9e9f792f9268ceb598e23
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832326"
---
# <a name="idiasessiongetsymbolsbyaddr"></a>IDiaSession::getSymbolsByAddr
检索查找符号按其地址的顺序的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT getSymbolsByAddr( 
   IDiaEnumSymbolsByAddr** ppEnumbyAddr
);
```

#### <a name="parameters"></a>参数
 `ppEnumbyAddr`

[out]返回[IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)对象。 使用此接口来搜索符号在符号存储区的内存位置。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)