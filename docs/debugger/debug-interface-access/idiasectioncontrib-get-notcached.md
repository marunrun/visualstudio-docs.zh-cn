---
title: 'Idiasectioncontrib:: Get_notcached |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_notCached method
ms.assetid: 5408ea53-f64c-431e-9f62-62819026b038
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dd58933146cea4a953c0c4290cebb0d12af8f199
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839662"
---
# <a name="idiasectioncontribgetnotcached"></a>IDiaSectionContrib::get_notCached
检索一个标志，指示是否不能缓存部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_notCached ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果不能缓存部分; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)