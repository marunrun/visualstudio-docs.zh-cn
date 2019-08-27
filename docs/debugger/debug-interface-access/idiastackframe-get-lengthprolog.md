---
title: IDiaStackFrame::get_lengthProlog | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_lengthProlog method
ms.assetid: 9894c5ca-835f-41e9-a35e-70e046dfb7f0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f9ebda7cf7336f9c6a9fc19babf9ed4bbc87fe43
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838101"
---
# <a name="idiastackframegetlengthprolog"></a>IDiaStackFrame::get_lengthProlog
检索块中的序言代码的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthProlog ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回的序言代码的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果不支持的属性。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)