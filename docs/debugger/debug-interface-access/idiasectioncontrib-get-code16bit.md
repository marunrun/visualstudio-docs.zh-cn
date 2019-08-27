---
title: IDiaSectionContrib::get_code16bit | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_code16bit method
ms.assetid: 8cde8fc5-9546-4f82-b4a8-afd0d835039e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d4e9c190108cdbf1eb7be2d21927a95fe56fca75
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832465"
---
# <a name="idiasectioncontribgetcode16bit"></a>IDiaSectionContrib::get_code16bit
检索一个标志，指示的部分是否包含 16 位代码。

## <a name="syntax"></a>语法

```C++
HRESULT get_code16bit(
   BOOL *pRetVal
};
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`部分中的代码是 16 位; 否则为如果返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法仅指示代码是否 16 位。 如果代码是不是 16 位，它可以是任何其他名字，例如 32 位或 64 位代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)