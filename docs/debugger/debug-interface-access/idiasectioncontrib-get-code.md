---
title: IDiaSectionContrib::get_code | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_code method
ms.assetid: f9ccf7a6-46e7-4a1d-9d5c-97272e17bbbb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8175fc05b05bfd3375fe0dcc0702741266801137
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828218"
---
# <a name="idiasectioncontribgetcode"></a>IDiaSectionContrib::get_code
检索一个标志，指示的部分是否包含可执行代码。

## <a name="syntax"></a>语法

```C++
HRESULT get_code ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`的部分包含可执行代码; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)