---
title: IDiaEnumSectionContribs::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Skip method
ms.assetid: 7471a178-5134-41b2-80a6-51ff96abe916
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cb371d841c10b64895400f66bf73159f27d68ec1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744255"
---
# <a name="idiaenumsectioncontribsskip"></a>IDiaEnumSectionContribs::Skip
跳过枚举序列中指定数量的节发布。

## <a name="syntax"></a>语法

```C++
HRESULT Skip( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 `celt`

中要跳过的枚举序列中的节发布数。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，如果没有更多要跳过的节内容，将返回 `S_FALSE`。

## <a name="see-also"></a>请参阅
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)