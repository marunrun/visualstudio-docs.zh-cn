---
title: IDiaStackWalker：： getEnumFrames |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalker2::getEnumFrames method
ms.assetid: f9f09729-4c34-441c-989c-e0b7339ee32c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd6f5219edf9426067a4431936caa2186604e1cc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741536"
---
# <a name="idiastackwalkergetenumframes"></a>IDiaStackWalker::getEnumFrames
检索 x86 平台的堆栈帧枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT getEnumFrames( 
   IDiaStackWalkHelper*   pHelper,
   IDiaEnumStackFrames**  ppEnum
);
```

#### <a name="parameters"></a>参数
 `pHelper`

中Helper [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)对象。

 `ppEnum`

弄返回一个[IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)对象，该对象包含一个[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)对象列表。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 若要获取任何其他平台上的堆栈帧列表，请调用[IDiaStackWalker：： getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)