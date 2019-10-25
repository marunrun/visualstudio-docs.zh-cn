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
ms.openlocfilehash: b1bd7e4963796858e7055667c1ae6a9557c77205
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739032"
---
# <a name="idiasymbolget_udtkind"></a>IDiaSymbol::get_udtKind
检索用户定义类型（UDT）的各种类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_udtKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回[UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)枚举中的一个值，该值指定 UDT 的类型：结构、类或联合。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)