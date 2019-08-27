---
title: 'Idiasymbol:: Get_hassecuritychecks |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasSecurityChecks method
ms.assetid: 4bb51f62-8645-41a4-bc44-1451010623fd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f5a760389f589dc14e8a768991323c0419dac527
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64808708"
---
# <a name="idiasymbolgethassecuritychecks"></a>IDiaSymbol::get_hasSecurityChecks
检索一个标志，指定是否已编译的编译单位或函数与缓冲区溢出安全检查 (例如， [/GS （缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)编译器开关)。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasSecurityChecks(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`如果函数具有任何安全检查; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [/GS（缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)