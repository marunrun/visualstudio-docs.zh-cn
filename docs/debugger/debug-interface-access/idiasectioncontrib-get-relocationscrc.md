---
title: IDiaSectionContrib::get_relocationsCrc | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_relocationsCrc method
ms.assetid: 8c29c91a-062d-4566-a9b7-49251036a15a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a57c46bef62039241c7d0cc064753199440893e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839506"
---
# <a name="idiasectioncontribgetrelocationscrc"></a>IDiaSectionContrib::get_relocationsCrc
检索的部分的重定位信息的循环冗余检查 (CRC)。

## <a name="syntax"></a>语法

```C++
HRESULT get_relocationsCrc ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回部分中的重定位信息的 CRC。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)