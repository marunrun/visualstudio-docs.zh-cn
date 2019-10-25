---
title: IDiaLoadCallback::NotifyOpenDBG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyOpenDBG method
ms.assetid: dbc4dcf0-4ace-4dce-9790-0fdaf3a23d3b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70607af90469594491223afa5f316dc63bf935b3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743071"
---
# <a name="idialoadcallbacknotifyopendbg"></a>IDiaLoadCallback::NotifyOpenDBG
在已打开候选的 dbg 文件时调用。

## <a name="syntax"></a>语法

```C++
HRESULT NotifyOpenDBG ( 
   LPCOLESTR dbgPath,
   HRESULT   resultCode
);
```

#### <a name="parameters"></a>参数
 `dbgPath`

中Dbg 文件的完整路径。

 `resultCode`

中指示应用到此文件的成功（`S_OK`）或负载失败的代码。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 通常会忽略返回代码。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)