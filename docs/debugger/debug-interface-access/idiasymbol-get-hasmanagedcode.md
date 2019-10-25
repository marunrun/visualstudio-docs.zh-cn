---
title: IDiaSymbol::get_hasManagedCode | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasManagedCode method
ms.assetid: e40f82f5-88fe-4a9b-b594-3605f42773ec
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 79696a0f4476d8e8b571cb8b8c0cc5e181b11f92
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740484"
---
# <a name="idiasymbolget_hasmanagedcode"></a>IDiaSymbol::get_hasManagedCode
检索一个标志，该标志指示该模块是否包含托管代码。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasManagedCode(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果模块包含托管代码，则返回 `TRUE`;否则，将返回 `FALSE`，代码为非托管代码。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 此属性可从 `SymTagCompilandDetails` 符号类型（请参阅[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)）中获取。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)