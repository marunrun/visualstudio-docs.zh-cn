---
title: IDiaSymbol::get_undecoratedName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedName method
ms.assetid: e49edf25-a51d-4787-bd5b-2bf5af827c8c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d9650c2ea67d847f225f047d62dd7d1867a61d4d
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64809173"
---
# <a name="idiasymbolgetundecoratedname"></a>IDiaSymbol::get_undecoratedName
检索的未修饰的名称C++进行修饰，或链接、 名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_undecoratedName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回的未修饰的名称C++修饰名。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)