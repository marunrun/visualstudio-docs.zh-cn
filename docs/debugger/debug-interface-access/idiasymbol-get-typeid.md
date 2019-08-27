---
title: IDiaSymbol::get_typeId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeId method
ms.assetid: b40be36e-10e1-463c-9c6d-21862679d29f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 007dd4ad4d7c0c06abf3c235753ec55febf3bcc3
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64800044"
---
# <a name="idiasymbolgettypeid"></a>IDiaSymbol::get_typeId
检索的符号的类型标识符。

## <a name="syntax"></a>语法

```C++
HRESULT get_typeId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回的符号的类型 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="remarks"></a>备注
 标识符是唯一的值创建的 DIA SDK，可将标记为唯一的所有符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)