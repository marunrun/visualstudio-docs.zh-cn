---
title: IDiaStackFrame::get_type | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_type method
ms.assetid: 99daa97b-5c05-455d-bd1e-800762ccf7c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b9a2a433c33d46215168238e9956ce0427171b24
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741569"
---
# <a name="idiastackframeget_type"></a>IDiaStackFrame::get_type
检索帧类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_type ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回[StackFrameTypeEnum 枚举](../../debugger/debug-interface-access/stackframetypeenum.md)枚举中的一个值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [StackFrameTypeEnum 枚举](../../debugger/debug-interface-access/stackframetypeenum.md)