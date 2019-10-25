---
title: IDiaSymbol：： get_hasSecurityChecks |Microsoft Docs
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
ms.openlocfilehash: 11fd7f70da9ae47b9858f8265d0608e3d6994ef7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740457"
---
# <a name="idiasymbolget_hassecuritychecks"></a>IDiaSymbol::get_hasSecurityChecks
检索一个标志，该标志指定是否已使用缓冲区溢出安全检查（例如， [/gs （缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)编译器开关）编译了编译单位或函数。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasSecurityChecks(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果函数有任何安全检查，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [/GS（缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)