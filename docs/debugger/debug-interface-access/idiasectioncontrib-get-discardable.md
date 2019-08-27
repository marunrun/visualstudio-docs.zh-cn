---
title: IDiaSectionContrib::get_discardable | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_discardable method
ms.assetid: 30ca88d4-3198-4b0f-b30e-2e54b3607fe9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ca50a9fa82f8db33fd12b5a94ee1fc9df7396124
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839545"
---
# <a name="idiasectioncontribgetdiscardable"></a>IDiaSectionContrib::get_discardable
检索一个标志，指示是否可以放弃部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_discardable ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果可以从内存丢弃部分中，根据需要; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)