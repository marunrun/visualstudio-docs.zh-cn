---
title: 'Idiasymbol:: Get_overloadedoperator |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_overloadedOperator method
ms.assetid: 257a9894-e980-47ae-bdc0-c5e2293ea734
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ecb56e35f376dc3c8046255499e9048c3758764
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64858473"
---
# <a name="idiasymbolgetoverloadedoperator"></a>IDiaSymbol::get_overloadedOperator
检索指定用户定义数据类型是否具有重载运算符的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_overloadedOperator ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果用户定义数据类型有重载的运算符; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)