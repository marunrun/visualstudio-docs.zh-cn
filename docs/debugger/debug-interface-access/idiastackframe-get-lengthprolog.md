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
ms.openlocfilehash: 7af0581f3278288c0acd0269a193b89b32b840c3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741700"
---
# <a name="idiastackframeget_lengthprolog"></a>IDiaStackFrame::get_lengthProlog
检索块中序言代码的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthProlog ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回序言代码的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)