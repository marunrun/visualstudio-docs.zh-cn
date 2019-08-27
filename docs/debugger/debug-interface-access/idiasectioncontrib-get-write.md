---
title: IDiaSectionContrib::get_write | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_write method
ms.assetid: 7e75348e-c12c-44ec-b004-e97767580a3f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cf20c4fe040155e6f2a88312b1fb0eab17e7f7df
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827607"
---
# <a name="idiasectioncontribgetwrite"></a>IDiaSectionContrib::get_write
检索一个标志，指示是否可以修改部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_write ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果部分可写; 否则为返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)