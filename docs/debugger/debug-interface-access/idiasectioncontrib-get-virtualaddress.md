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
ms.openlocfilehash: 6e5c3fb1615e76dbe3799fda0773a084dd1c4ac7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742492"
---
# <a name="idiasectioncontribget_virtualaddress"></a>IDiaSectionContrib::get_virtualAddress
检索贡献的虚拟地址（VA）。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回贡献的 VA。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)