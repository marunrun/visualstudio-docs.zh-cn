---
title: IDiaLoadCallback::RestrictSymbolServerAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::RestrictSymbolServerAccess method
ms.assetid: db37ad9f-f75e-4f0c-83bf-21a6e66ba859
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 87d590af5162d3efd2ef2c9702a3fe9f45250993
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743024"
---
# <a name="idialoadcallbackrestrictsymbolserveraccess"></a>IDiaLoadCallback::RestrictSymbolServerAccess
确定是否允许访问符号服务器来解析符号。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictSymbolServerAccess();
```

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 除 `S_OK` 以外的任何返回代码均可防止使用符号服务器解析符号。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)