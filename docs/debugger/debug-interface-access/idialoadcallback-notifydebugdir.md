---
title: IDiaLoadCallback::NotifyDebugDir | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyDebugDir method
ms.assetid: bd04e2f6-0dbf-4742-a556-96f2cd99aa19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6618440cab9b9042ec371383f6c809ca1d0d11f7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743091"
---
# <a name="idialoadcallbacknotifydebugdir"></a>IDiaLoadCallback::NotifyDebugDir
在 .exe 文件中找到调试目录时调用。

## <a name="syntax"></a>语法

```C++
HRESULT NotifyDebugDir ( 
   BOOL  fExecutable,
   DWORD cbData,
   BYTE  data[]
);
```

#### <a name="parameters"></a>参数
 `fExecutable`

[in] 如果调试目录是从可执行文件（而不是一个 dbg 文件）读取，则 `TRUE`。

 `cbData`

中调试目录中数据的字节计数。

 `data[]`

中用调试目录填充的数组。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 通常会忽略返回代码。

## <a name="remarks"></a>备注
 当处理可执行文件时， [IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法会调用此回调。

 此方法不再需要客户端对可执行文件和/或调试文件进行反向工程以支持除 .pdb 文件中找到的信息以外的调试信息。 使用此数据，客户端可以识别可用的调试信息的类型，以及它是位于可执行文件中还是在 dbg 文件中。

 大多数客户端不需要此回调，因为 `IDiaDataSource::loadDataForExe` 方法在必要时可以透明地打开 .pdb 和 dbg 文件以提供符号。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)