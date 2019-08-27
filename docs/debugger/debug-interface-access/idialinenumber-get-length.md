---
title: 'Idialinenumber:: Get_length |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_length method
ms.assetid: 2c55a6f7-4ef5-45fb-9fd1-d72deaaa2829
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 896e26075780c0cbd7bf0b1762da141d5ba7d2d1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828473"
---
# <a name="idialinenumbergetlength"></a>IDiaLineNumber::get_length
检索在块中的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_length ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]在块中返回字节的数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 块是在行上的源代码的长度由[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)对象。

## <a name="see-also"></a>请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)