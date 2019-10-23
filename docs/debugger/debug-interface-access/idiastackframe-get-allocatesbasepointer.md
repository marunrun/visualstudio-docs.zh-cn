---
title: IDiaStackFrame::get_allocatesBasePointer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_allocatesBasePointer
ms.assetid: a91e9c8e-c5e3-4887-a60b-f03b5a98f30c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6710a20bb5a01d3d342c31b48f1f96e7e2a2062a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741765"
---
# <a name="idiastackframeget_allocatesbasepointer"></a>IDiaStackFrame::get_allocatesBasePointer
检索一个标志，该标志指示是否为此地址范围内的代码分配基指针。

## <a name="syntax"></a>语法

```C++
HRESULT get_allocatesBasePointer ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果为此帧中的代码分配了基指针，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)