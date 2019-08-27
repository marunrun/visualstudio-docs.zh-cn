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
ms.openlocfilehash: 97ca8b06a480d2fddb2002a0b9a19f878caa58f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828596"
---
# <a name="idialoadcallbacknotifyopendbg"></a>IDiaLoadCallback::NotifyOpenDBG
当打开候选.dbg 文件时调用。

## <a name="syntax"></a>语法

```C++
HRESULT NotifyOpenDBG ( 
   LPCOLESTR dbgPath,
   HRESULT   resultCode
);
```

#### <a name="parameters"></a>参数
 `dbgPath`

[in].Dbg 文件的完整路径。

 `resultCode`

[in]指示是否成功的代码 (`S_OK`) 或失败的负载应用到此文件。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回代码通常被忽略。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)