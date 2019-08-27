---
title: IDiaSectionContrib::get_relativeVirtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_relativeVirtualAddress method
ms.assetid: 32f9674d-94f1-4590-99de-a2eb60da4af8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5469bcf8b40dffad0e8a84446d11e3e5eb71e0d0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827715"
---
# <a name="idiasectioncontribgetrelativevirtualaddress"></a>IDiaSectionContrib::get_relativeVirtualAddress
检索的映像相对虚拟地址 (RVA) 所占比例。

## <a name="syntax"></a>语法

```C++
HRESULT get_relativeVirtualAddress ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回图像中所占的 RVA。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)