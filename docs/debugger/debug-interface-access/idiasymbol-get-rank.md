---
title: 'Idiasymbol:: Get_rank |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_rank method
ms.assetid: 14cc9c4b-a5ec-414a-b01f-4a142c17b7cc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c38962ab5915a4235201e76e1828f84a56af1333
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64830786"
---
# <a name="idiasymbolgetrank"></a>IDiaSymbol::get_rank
检索 FORTRAN 多维数组的秩 （维数）。

## <a name="syntax"></a>语法

```C++
HRESULT get_rank ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]FORTRAN 多维数组中返回维度的数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 级别是指其中的数组声明为数组中的维度数量`myarray[1,2,3]`。 此示例具有排名为 3 到 3 个维度。 排名不适用于C++使用每个维度的数组的数组的概念 (即`myarray[1][2][3]`)。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)