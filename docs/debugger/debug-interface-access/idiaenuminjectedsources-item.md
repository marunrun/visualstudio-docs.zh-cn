---
title: IDiaEnumInjectedSources::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources::Item method
ms.assetid: 14846955-7270-451d-91d2-9cb34bb65187
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2fd803520a6b6bb58679dd30dbf913450ce6066a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833565"
---
# <a name="idiaenuminjectedsourcesitem"></a>IDiaEnumInjectedSources::Item
通过索引中检索的插入的源。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD                index,
   IDiaInjectedSource** injectedSource
);
```

#### <a name="parameters"></a>参数
 索引

[in]索引[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)要检索对象。 索引是范围 0 到`count`-1，其中`count`返回的[idiaenuminjectedsources:: Get_count](../../debugger/debug-interface-access/idiaenuminjectedsources-get-count.md)方法。

 injectedSource

[out]返回[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)对象，表示插入的源。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)