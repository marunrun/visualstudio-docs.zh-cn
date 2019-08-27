---
title: IDiaLineNumber::get_columnNumber | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_columnNumber method
ms.assetid: e317f29a-6525-46a7-8421-33985392f8fd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 03d24770c90ebd225fa37dd7f60d794781e79e7e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828450"
---
# <a name="idialinenumbergetcolumnnumber"></a>IDiaLineNumber::get_columnNumber
检索表达式或语句的开始处的列号。

## <a name="syntax"></a>语法

```cpp
HRESULT get_columnNumber ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回表达式或语句的开始处的列号。 如果值为零，则不存在的列信息。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的列的值是语句的在行中的第一个字符到行的字节的偏移量。

## <a name="see-also"></a>请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)