---
title: EndTrackingContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- EndTrackingContext
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- EndTrackingContext
ms.assetid: c2c5d794-8dc8-4594-8717-70dc79a0e75d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b7f837e7a983d0f2c2520d7e379ffb49f332c75c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62821112"
---
# <a name="endtrackingcontext"></a>EndTrackingContext
结束当前跟踪上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT WINAPI EndTrackingContext();
```

## <a name="return-value"></a>返回值
如果跟踪上下文结束，返回带 SUCCEEDED  位组的 HRESULT  。

## <a name="requirements"></a>要求
**标头：** FileTracker.h 

## <a name="see-also"></a>请参阅
- [StartTrackingContext](../msbuild/starttrackingcontext.md)
