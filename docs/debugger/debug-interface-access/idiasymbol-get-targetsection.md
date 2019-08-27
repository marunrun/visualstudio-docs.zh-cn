---
title: 'Idiasymbol:: Get_targetsection |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_targetSection method
ms.assetid: 95382395-da41-4aa8-87f1-5b03da128565
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1dcfd72d7cd4cca527c2318b0c3c412020457e8e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64821025"
---
# <a name="idiasymbolgettargetsection"></a>IDiaSymbol::get_targetSection
检索转换 （thunk） 目标的地址部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_targetSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]部分的转换 （thunk） 目标地址的一部分。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)