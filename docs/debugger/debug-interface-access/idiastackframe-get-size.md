---
title: IDiaStackFrame::get_size | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_size method
ms.assetid: 71e2f5ab-4aa8-4922-aa8a-b7db97ee143c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6728418e848941bb537f5bec4cb4f772c73485c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832048"
---
# <a name="idiastackframegetsize"></a>IDiaStackFrame::get_size
检索以字节为单位的堆栈帧的大小。

## <a name="syntax"></a>语法

```C++
HRESULT get_size ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]以字节为单位返回堆栈帧的大小。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果不支持的属性。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)