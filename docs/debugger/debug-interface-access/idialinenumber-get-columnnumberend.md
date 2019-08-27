---
title: IDiaLineNumber::get_columnNumberEnd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_columnNumberEnd method
ms.assetid: 02fa56c1-87b6-405a-adee-3bb6bc62de2d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 567df436093b53432e44e21fb96f0d092b71c81d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839844"
---
# <a name="idialinenumbergetcolumnnumberend"></a>IDiaLineNumber::get_columnNumberEnd
检索表达式或语句的结束位置基于 1 的源列数。

## <a name="syntax"></a>语法

```C++
HRESULT get_columnNumberEnd ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回的列号的表达式或语句的结束位置。 如果值为零，则不存在列结束信息。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的列值是语句的字节偏移量之后的行的最后一个字符的位置的行。

## <a name="see-also"></a>请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)