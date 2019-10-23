---
title: IDiaSession::findFileById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findFileById method
ms.assetid: 710efe04-78b5-4f3e-a1d8-f9b069063503
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aafdd2270606ba6e56713e9166dbae2b8c635b41
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742265"
---
# <a name="idiasessionfindfilebyid"></a>IDiaSession::findFileById
按源文件标识符检索源文件。

## <a name="syntax"></a>语法

```C++
HRESULT findFileById ( 
   DWORD            uniqueId,
   IDiaSourceFile** ppResult
);
```

#### <a name="parameters"></a>参数
 `uniqueId`

中指定源文件标识符。

 `ppResult`

弄返回一个[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象，该对象表示检索到的源文件。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 源文件标识符是 DIA SDK 内部使用的唯一值，用于使所有源文件唯一。 此方法通常在内部用于 DIA SDK。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)