---
title: IDiaSymbol::get_typeIds | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeIds method
ms.assetid: 5166e647-fde5-4efe-92bf-77f8ae3fbc9b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7b32ab5b1965ea7a641cfac470addd2aae0ede0
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64791762"
---
# <a name="idiasymbolgettypeids"></a>IDiaSymbol::get_typeIds
检索此符号的特定于编译器的类型标识符值的数组。

## <a name="syntax"></a>语法

```C++
HRESULT get_typeIds ( 
   DWORD  cTypeIds,
   DWORD* pcTypeIds,
   DWORD  typeIds[]
);
```

#### <a name="parameters"></a>参数
 `cTypeIds`

[in]若要保存的数据缓冲区的大小。

 `pcTypeIds`

[out]返回的数`typeIds`编写的或者，如果`typeIds`是`NULL`，然后提供的类型标识符的总数。

 `typeIds[]`

[out]若要使用的类型标识符填充数组。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)