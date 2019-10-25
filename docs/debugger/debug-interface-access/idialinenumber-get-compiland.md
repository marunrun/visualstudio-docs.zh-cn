---
title: IDiaLineNumber：： get_compiland |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_compiland method
ms.assetid: c476d0b8-c473-47eb-96f5-c4e8f577b1c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d6ae842d4717bdc0bd989327f07d9566d1161b8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743233"
---
# <a name="idialinenumberget_compiland"></a>IDiaLineNumber::get_compiland
检索提供图像文本字节的编译单位的符号引用。

## <a name="syntax"></a>语法

```C++
HRESULT get_compiland ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

弄返回提供图像文本字节的编译单位的[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)