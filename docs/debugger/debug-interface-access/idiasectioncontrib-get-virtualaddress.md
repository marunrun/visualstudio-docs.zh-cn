---
title: IDiaSectionContrib::get_virtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_virtualAddress method
ms.assetid: e5b44a81-0804-429b-97d8-467cbba3132a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ea896164d19ca518205ace95b9945abb0bf7c501
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839493"
---
# <a name="idiasectioncontribgetvirtualaddress"></a>IDiaSectionContrib::get_virtualAddress
检索所占比例的虚拟地址 (VA)。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回所占比例的 VA。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)