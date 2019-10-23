---
title: IDiaStackFrame::get_returnAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_returnAddress method
ms.assetid: 0df91981-919f-48ed-9c70-4121567d645b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5312eb455de8ce187bf4ae2acc2fc5b4b57a07bc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741608"
---
# <a name="idiastackframeget_returnaddress"></a>IDiaStackFrame::get_returnAddress
检索帧的返回地址。

## <a name="syntax"></a>语法

```C++
HRESULT get_returnAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回帧的返回地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)