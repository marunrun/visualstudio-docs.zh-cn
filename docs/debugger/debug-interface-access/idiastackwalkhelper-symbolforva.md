---
title: IDiaStackWalkHelper::symbolForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::symbolForVA method
ms.assetid: 8dd9455d-d44c-4dd6-a0aa-31131cbea2aa
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f646616fddc0e7727ef9e8e80d9c29fbcba6ebc0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741323"
---
# <a name="idiastackwalkhelpersymbolforva"></a>IDiaStackWalkHelper::symbolForVA
检索包含指定虚拟地址的符号。

## <a name="syntax"></a>语法

```C++
HRESULT symbolForVA( 
   ULONGLONG     va,
   IDiaSymbol**  ppSymbol
);
```

#### <a name="parameters"></a>参数
 `va`

中请求的符号中包含的虚拟地址。 符号必须是 `SymTagFunctionType` （ [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举中的值）。

 `ppSymbol`

弄一个[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，它表示指定地址处的符号。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)