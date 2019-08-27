---
title: 'Idiaenumlinenumbers:: Skip |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Skip method
ms.assetid: d182c269-8c76-4d8b-8275-c6807c5ae4e1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e68eccfebfc5218d59649aa09162b20467ceb670
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554009"
---
# <a name="idiaenumlinenumbersskip"></a>IDiaEnumLineNumbers::Skip
将跳过指定的数目的枚举序列中的行号。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

[in]枚举序列中的行号以跳过数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`是否存在要跳过的多个行号。

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)