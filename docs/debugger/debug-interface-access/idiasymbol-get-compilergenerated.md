---
title: IDiaSymbol：： get_compilerGenerated |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_compilerGenerated method
ms.assetid: 864d9249-f0c8-4a34-b391-eb785f7e8865
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c67a3ae78db3f91f25f69c1045856c5d167c2d34
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740821"
---
# <a name="idiasymbolget_compilergenerated"></a>IDiaSymbol::get_compilerGenerated
检索一个标志，该标志指示符号是否是由编译器生成的。

## <a name="syntax"></a>语法

```C++
HRESULT get_compilerGenerated ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果编译器生成了符号，则返回 `TRUE`;否则，如果从用户编写的源生成符号，则将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)