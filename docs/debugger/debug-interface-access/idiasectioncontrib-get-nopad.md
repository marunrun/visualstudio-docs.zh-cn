---
title: IDiaSectionContrib::get_nopad | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_nopad method
ms.assetid: f5c08603-0b3e-4e81-acf1-1b95a6a83bed
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 51fb2c4ff2f27cee8fcc989139f5ae14c2641394
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828097"
---
# <a name="idiasectioncontribgetnopad"></a>IDiaSectionContrib::get_nopad
检索一个标志，指示是否在部分应不填充到下一个内存边界。

## <a name="syntax"></a>语法

```C++
HRESULT get_nopad(
   BOOL* pRetVal
};
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果部分应不填充到下一步的内存边界; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 这是通常会出现仅在较旧的文件上的属性。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)