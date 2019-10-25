---
title: IDiaSectionContrib::get_remove | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_remove method
ms.assetid: fd30ab7b-022b-4402-a42a-2d38e274c1b1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0b21423dc017a09b983ae157774aa4f0485df1a9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742529"
---
# <a name="idiasectioncontribget_remove"></a>IDiaSectionContrib::get_remove
检索一个标志，该标志指示是否在部分成为内存中映像的一部分之前删除该部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_remove ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果不将节添加到内存中的映像，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)